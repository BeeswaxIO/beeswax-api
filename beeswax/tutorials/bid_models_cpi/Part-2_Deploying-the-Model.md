# Part 2: Deploying the Model
We now have our final version of the model, we want to actually turn it into a Beeswax Bid Model.  To do that, we need to take the following steps:
* Generate the Prediction Files
* Generate the Manifest File
* Upload to Beeswax via the Buzz API

We'll start with the Prediction Files.

### Generate the Prediction Files
Bid Models are represented as a set of data files referred to as "Prediction Files". Each file has the following configuration:
* pipe-delimited ("|") text files
* no compression
* first row of each file contains headers
* at least one "feature" field
* a required field called "value", which represents either the CPM Bid or Bid Multiplier for that row 
* null values should be left blank
* max file size of 100MB (can upload as many files as you like)

Our prediction files will look something like this:

| app_bundle | display_manager | placement_type   | banner_height | platform_os_version | value          |
|------------|-----------------|------------------|---------------|---------------------|----------------|
| 1005765746 | Fyber           | BANNER           | 320           | 4.1                 | expected bid |
| 1008508212 | SOMA            | BANNER           | 320           | 11.0                | expected bid |
| 1016562846 | AerservSDKiOS   | BANNER_AND_VIDEO | null          | 12.0                | expected bid |
| ...        | ...             | ...              | ...           | ...                 | ...            |
    
We want to make sure that we have a prediction for any auction we may want to bid on. To do that, we are going to grab some auction logs and run them through our SageMaker model endpoint to get the probability of conversion and then multiply by our convesion value to get to our actual bid price.

Let's start by loading our auction logs.

```python
BUCKET = 'beeswax-data-us-east-1'
AUCTION_LOGS_PATH = 'raw-logs-export/canary/auction/yyyy=2019/MM=03/'
NUMFILES = -40000

client = boto3.client('s3')
resource = boto3.resource('s3')
bucket = resource.Bucket(BUCKET)

fs = s3fs.S3FileSystem()

auction_files = list(bucket.objects.filter(Prefix=AUCTION_LOGS_PATH))
auction_frames = []
for _file in auction_files[NUMFILES:]:
    if not _file.key.endswith('gz'):
        continue
    with fs.open('s3://{}/{}'.format(BUCKET, _file.key)) as f:
        df = pd.read_csv(f, compression='gzip', header=0, sep=',', quotechar='"')
        auction_frames.append(df[['ad_position','app_bundle','app_id','app_name','auction_type',
                 'platform_bandwidth', 'banner_height','banner_width','platform_browser',
                 'platform_browser_version','platform_carrier','geo_city','content_rating',
                 'content_coppa_flag','geo_country','platform_device_make','platform_device_model',
                 'platform_device_screen_size','platform_device_type','display_manager',
                 'display_manager_ver','domain','environment_type','inventory_interstitial',
                 'inventory_source','platform_js','content_language','geo_metro','platform_os',
                 'platform_os_version','placement','placement_type','publisher_id','geo_region',
                 'site_name','site_id','geo_zip', 'exchange_predicted_view_rate', 'rewarded', 
                 'video_boxing_allowed', 'video_companion_required','geo_lat', 'geo_long', 'video_playback_method',
                 'video_player_size', 'video_start_delay', 'bid_time_epoch_in_usecs']])
auction_df = pd.concat(auction_frames, axis=0, ignore_index=True)
```

We've got some auction logs, so now we need to make the auction logs match the input for our model endpoint. To do this, we'll take this data through all the transformations we took the original win/conversion files through.

##### 1) fill na values with -1 and select unique rows


```python
auction_df = auction_df.fillna(-1).drop_duplicates()
```
##### 2) replace calculated fields


```python
auction_df['hour_of_day_utc'] = pd.to_datetime(auction_df['bid_time_epoch_in_usecs'], unit='us')
auction_df['hour_of_day_utc'] = auction_df['hour_of_day_utc'].dt.hour
auction_df['lat_long_present'] = pd.notna(auction_df['geo_lat'])
auction_df = auction_df.drop(['bid_time_epoch_in_usecs', 'geo_lat', 'geo_long'], axis = 1).drop_duplicates()
```

##### 2) drop unneeded fields


```python
with open('data/prod_model.json', 'r') as f:
    prod_model = json.loads(f.read())
    
needed_fields = set([col.split('-')[0] for col in prod_model['features']])
auction_df = auction_df[list(needed_fields)]
```
##### 4) convert field data types
```python
# we don't really have any continuous features, so we'll convert most numeric fields to strings
for column in auction_df.select_dtypes(include=['int64','float64', 'bool']).columns:
    if column in ['lat_long_present']:
        auction_df[column] = auction_df[column].astype('int64')
    auction_df[column] = auction_df[column].astype('object')
```

##### 5) one-hot encoded data
```python
auction_df_dummies = pd.get_dummies(auction_df.to_sparse(), sparse=True, prefix_sep='-')
```

##### 6) merge columns
Our model expects a specific number of columns in a specific order and this auction data, because of the one-hot encoding contains some separate set of columns.  To make this score-able in our model, we need to make sure the columns match exactly. For each column in the trained model we will:
* use the column from our auction data if it exists
* if it does not exist, we will create the column and set the values to all 0
* drop any additional columns from our auction data (they won't result in any score from our model anyway)


```python
cols = list(set(prod_model['features']) & set(auction_df_dummies.columns))
auction_df_dummies = auction_df_dummies[cols]
auction_df_dummies = auction_df_dummies.to_dense()
auction_df_dummies = auction_df_dummies.loc[:,~auction_df_dummies.columns.duplicated()]
data_to_score = pd.DataFrame().reindex_like(auction_df)


# merge in all the existing columns
for feature in prod_model['features']:
    try:
        data_to_score[feature] = auction_df_dummies[feature]
    except KeyError:
        data_to_score[feature] = 0
    except ValueError:
        print('{} is duplicated'.format(feature))

# rearrange the columns and drop the unsupported ones
data_to_score = data_to_score[prod_model['features']]
```
Now the data is prepared for scoring. Using our prediction function from previous tutorials, let's go ahead and generate our predictions:

```python
from sagemaker.transformer import Transformer

data_to_score.to_csv('data/predictions/input.csv', index=False, header=False)

bucket = 'beeswax-tmp-us-east-1'
prefix = 'bid-models-test-data/canary/sagemaker'
output = 's3://{}/{}/predictions/output'.format(bucket, prefix)
input_location = 's3://{}/{}/predictions/input.csv'.format(bucket, prefix)
boto3.Session().resource('s3').Bucket(bucket).Object(os.path.join(prefix, 'predictions/input.csv')).upload_file('data/predictions/input.csv')

transformer = Transformer(
    base_transform_job_name='Batch-Transform',
    model_name='linear-learner-2019-03-23-16-50-13-882',
    instance_count=1,
    instance_type='ml.c5.xlarge',
    output_path=output
)

transformer.transform(input_location, content_type='text/csv', split_type='Line')
transformer.wait()

key = prefix + '/predictions/output/input.csv.out'
boto3.resource('s3').Bucket(bucket).download_file(key, './data/predictions/output.csv')

results = []
with open('./data/predictions/output.csv', 'r') as f:
    output = f.readlines()
    for row in output:
        results.append(json.loads(row)['score'])

auction_df['prediction'] = results
```

    INFO:sagemaker:Creating transform job with name: Batch-Transform-2019-03-25-18-31-12-705
    ...............................................!


We now have predictions for each row auction logs we loaded.  Let's see what they look like by ploting them on a histogram:

```python
print(auction_df['prediction'].describe())
auction_df['prediction'].hist(bins=1000)
```

    count    904841.000000
    mean          0.038641
    std           0.026349
    min          -0.096586
    25%           0.014953
    50%           0.044258
    75%           0.058983
    max           0.194851
    Name: prediction, dtype: float64


So, immediately, we notice that the predictions are reasonably distributed, which is good, but a significant number of the predictions are below 0. We obviously can't bid below 0, so let's normalize our predictions by replacing any values below 0 with 0:


```python
auction_df['prediction'] = auction_df['prediction'].fillna(0)
auction_df.loc[auction_df['prediction'] < 0.0, 'prediction'] = 0
auction_df['prediction'].hist(bins=100)
```


Okay that's better.  Now let's calculate our actual CPM bids. Recall that we will calculate our bid as follows:

>conversion_value * likelihood_of_conversion = bid_price

We also need to express our bid as a cpm, so we will update our formula to the following:

>conversion_value * likelihood_of_conversion * 1000 = bid_price

And finally, we can substitute in our conversion value:

>5 * likelihood_of_conversion * 1000 = bid_price


```python
auction_df['value'] = auction_df['prediction']*5*1000
auction_df['value'].hist(bins=100)
```


Now we have bids. You'll notice that we have some very high bids for some rows, probably higher than they need to be for us to win.  We'll set a "max bid" when we upload this so we don't have to worry about capping in the model itself.

Okay, we have our prediction data ready, now let's get it ready for upload:

1) remove all the "-1" values (they can just be empty strings)
```python
auction_df = auction_df.drop(['prediction'], axis=1)
auction_df = auction_df.replace(to_replace=-1, value='')
```

2) drop any data with invalid rows
```python
# make sure we don't have any unsupported ENUM values
auction_df = auction_df.loc[auction_df['platform_bandwidth'].isin(['CONNECTION_UNKNOWN', 'ETHERNET', 'WIFI', 'CELL_UNKNOWN', 'CELL_2G', 'CELL_3G', 'CELL_4G', ''])]
auction_df = auction_df.loc[~auction_df['inventory_source'].isin(['0'])]

# make sure metro fields are valid
auction_df['geo_metro'] = auction_df['geo_metro'].fillna('')
auction_df = auction_df[~auction_df['geo_metro'].apply(lambda x: len(x)>5)]
auction_df['geo_metro'] = auction_df['geo_metro'].astype('int')

# make sure all interger fields are integers and not doubles
int_fields = ('banner_height', 'banner_width', 'day_of_week_utc', 'hour_of_day_utc',
              'rewarded', 'auction_type', 'video_companion_required', 'content_coppa_flag',
              'inventory_interstitial', 'platform_js', 'lat_long_present', 'video_start_delay')
for col in auction_df:
    if col not in int_fields:
        continue
    auction_df[col] = auction_df[col].replace(to_replace='', value='-100')
    auction_df[col] = auction_df[col].astype('int64')
    auction_df[col] = auction_df[col].replace(to_replace='-100', value='')

# make sure every row has a value
auction_df['value'] = auction_df['value'].replace(to_replace='', value='0.0')
auction_df['value'] = auction_df['value'].fillna(0.0)
```

3) create CSV files to upload, and upload them to S3
```python
auction_df.to_csv('data/predictions/predictions.csv', index=False, header=True, sep='|')

timestamp = int(time.time())
bucket = 'beeswax-data-us-east-1'
prefix = 'bid_models/canary/customer_data_files/sagemaker/'
prediction_path = os.path.join(prefix, 'predictions-{}.csv'.format(timestamp))
boto3.Session().resource('s3').Bucket(bucket).Object(prediction_path).upload_file('data/predictions/predictions.csv')
```

### Generate the Manifest File

The manifest file tells Beeswax where to find, and how to interpret your prediction files. This file is a .json file and should have the following format:

```{
    "model_predictions": [
        "<S3 path to prediction file>",
        "<S3 path to prediction file>",
        ...
    ],
    "metadata": {
        "fields": [
            "<field name>",
            "<field name>",
            ...
        ]
    }
}```

We can easily generate this from our existing data and upload it to S3:


```python
features = list(auction_df.drop(['value'], axis=1).columns)
manifest = {
    'model_predictions': [
        's3://{}/{}'.format(bucket, prediction_path)
    ],
    'metadata': {
        'fields': features
    }
}

with open('data/predictions/manifest.json', 'w') as f:
    f.write(json.dumps(manifest))

prefix = 'bid_models/canary/customer_manifests/sagemaker/'
manifest_path = os.path.join(prefix, 'manifest-{}.csv'.format(timestamp))
boto3.Session().resource('s3').Bucket(bucket).Object(manifest_path).upload_file('data/predictions/manifest.json')
```

### Upload to Buzz

We've reached the final step and its time to actually upload our model to Beeswax via the [Buzz API](https://docs.beeswax.com). To do this, we will first create a `bid_model` object ([docs](https://docs.beeswax.com/docs/bid-models-overview)) and attach a `bid_model_version` ([docs](https://docs.beeswax.com/docs/bid-model-versions-overview)) that points to our predictions, then we will attach the Bid Model to a Bid Modifier.

These steps can all be done via the UI as well, but since we've written everything else in Python we might as well do our upload that way as well. Note, you must replace `yourendpoint` with the correct host provided by Beeswax.

First, authenticate:

```python
s = requests.Session()
payload = {
    'email': buzz_username,
    'password': buzz_password,
    'keep_logged_in': True
}
s.post('https://yourendpoint.api.beeswax.com/rest/authenticate', json=payload)
```

Then create the `bid_model` object.  We will use the `value_type` "BID", but could also specify "MULTIPLIER" if we wanted the value to be multiplied into the base bid for the bidding strategy we will select later.


```python
payload = {
    'active': True,
    'bid_model_name': 'cpi_tutorial-{}'.format(timestamp),
    'value_type': 'BID'
}
response = s.post('https://yourendpoint.api.beeswax.com/rest/bid_model', json=payload)
bid_model_id = response.json()['payload']['id']
```

Next, we need to attach a `bid_model_version` to our `bid_model`.  This is where we will actually tell Beeswax about our manifest file:


```python
payload = {
    'active': True,
    'bid_model_id': response.json()['payload']['id'],
    'bid_model_version_name': 'cpi_tutorial-v_{}'.format(timestamp),
    'manifest_s3_path': 's3://{}/{}'.format(bucket, manifest_path)
}
response = s.post('https://yourendpoint.api.beeswax.com/rest/bid_model_version', json=payload)
version_id = response.json()['payload']['id']
```

Next, update the `bid_model` to tell it which version to use (the one we just created):


```python
payload = {
    'bid_model_id': bid_model_id,
    'current_version': version_id
}
response = s.put('https://yourendpoint.api.beeswax.com/rest/bid_model', json=payload)
```

Next, create a `bid_modifier` and attach the `bid_model` to it:
```python
payload = {
    'active': True,
    'bid_model_id': bid_model_id,
    'bid_modifier_name': 'cpi_tutorial-{}'.format(timestamp)
}
response = s.post('https://yourendpoint.api.beeswax.com/rest/bid_modifier', json=payload)
bid_modifier_id = response.json()['payload']['id']
```

Congratulations! We've trained, tuned and deployed a live Bid Model to the Beeswax platform. At this point the Bid Model is ready to use with a campaign; just attach it to a line item like any other Bid Modifier!

Hopefully this tutorial has given you the basics required to get started. If you're interested in more detail, you can find the full Jupyter notebooks for this tutorial in the ["notebooks"](https://github.com/BeeswaxIO/beeswax-api/blob/beeswax/tutorials/bid_models_cpi/notebooks/) directory.  These notebooks include additional steps that we left out of this tutorial like hyperparameter tuning and evaluating feature importance.

There are a few topics that we haven't discussed at all, but plan to cover in the future:
* Monitoring a live model and making updates to improve performance
* Factoring in auction dynamics such as auction type (1st vs 2nd), market price estimation, etc
* Using a Bid Model in conjunction with device level scores.

Stay tuned!


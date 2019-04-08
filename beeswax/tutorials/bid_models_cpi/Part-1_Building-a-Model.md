# Part 1: Building a Model
## Data Prep
Before we actually train our model, we need to prepare some data for it. This has two steps:

1) Gather and Clean Some Data
For our CPI model, we will be using Beeswax [Win and Conversion logs](https://docs.beeswax.com/docs/data-feeds) as our input dataset. These datasets contain all the possible features we could use in our model. Our data is already pretty clean since its in a structured format as dictated by the log formats. Therefore, our "cleansing" process is really focused on eliminating any data that will negatively effect our model.  We want to a) eliminate any outliers from the data and b) remove any columns which we may not need (for example, we don't need `domain` if we're only buying mobile)

2) Prepare the Data for Modeling
Once we have our raw data, we need to transform it into a format that can be used be used in our model:
* In our CPI model, we ultimately want to predict a likeliness that a given bid request will lead to an app install so we need to put this probability metric into our dataset. We'll aggregate the logs so that every unique combination of keys occurs once and then calculate `conversion_rate` as `conversions`/`impressions`.
* Most of the variables in a bid request are categorical.  In order for our regression models to understand them, we'll need to convert them to numeric variables through a process called [one-hot encoding](https://www.kaggle.com/dansbecker/using-categorical-data-with-one-hot-encoding).
* We also need to split the data so that we have separate datasets for training the model, validating the model, and then testing the model once its built.

Let's pick up the modeling process after these steps (if you want to see how this is done, check [here](https://github.com/BeeswaxIO/beeswax-api/blob/master/beeswax/tutorials/bid_models_cpi/notebooks/bid-model-tutorial_step-1.ipynb)). At this point we have a dataset that looks like the below, and we have it split into train/test/validation sets written to S3.

|conversion_rate|ad_position_ABOVE_THE_FOLD|ad_position_FULLSCREEN|ad_position_POSITION_UNKNOWN|app_bundle_1040200670|app_bundle_1089048531|app_bundle_1092689152|app_bundle_1114751883|app_bundle_1118431695|app_bundle_1177418991|...|hour_of_day_utc_16|hour_of_day_utc_17|hour_of_day_utc_18|hour_of_day_utc_19|hour_of_day_utc_20|hour_of_day_utc_21|hour_of_day_utc_22|hour_of_day_utc_23|lat_long_present_0|lat_long_present_1|
|--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |--- |---|
|0.243056|1|0|0|0|0|0|0|0|0|...|0|0|0|1|0|0|0|0|1|0|
|0.203883|1|0|0|0|0|0|0|0|0|...|0|0|0|0|1|0|0|0|1|0|
|0.287879|1|0|0|0|0|0|0|0|0|...|0|0|0|0|0|0|0|0|1|0|
|0.307692|1|0|0|0|0|0|0|0|0|...|1|0|0|0|0|0|0|0|1|0|
|0.235294|1|0|0|0|0|0|0|0|0|...|0|0|0|0|0|0|0|0|1|0|

# Model Training
At this point, we want to actually build some predictive models. We might try to fit many different models and see what performs the best. However, for the sake of keeping this tutorial as brief as possible, we'll use a multi-variate linear regression model. Most people will be familiar with linear regression from their "intro to statistics" days, but the basic gist of it is that we will assign some coefficient to each feature in the model such that the aggregate sum of features multiplied by their coefficients is our `conversion_rate` prediction.

We will then evaluate our model as follows:
* We'll train our model with our "train" and "validation" datasets
* We'll then use our model to generate predictions for our "test" dataset
* We'll calculate the difference between the actual and predicted `conversion_rate` for each row, our "error"
* We'll calculate the "mean absolute error" (MAE) from these values. The lower the MAE, the more accurate the model. 

Since SageMaker has a built in `linear learner` model, we can use the AWS modeling APIs to train our model and then deploy an endpoint to score our test data against it.  This is a big advantage because we don't need to worry about deploying infrastructure... we just point the api at our data and get a model back.  That said, if you are used to other modeling tools, those will work as well.

First, let's setup the model by giving it some basic parameters and telling it where to put its output:

```python
container = get_image_uri(boto3.Session().region_name, 'linear-learner')
train_data = pd.read_pickle('./data/step2-train.pkl')

bucket = 'beeswax-tmp-us-east-1'
prefix = 'bid-models-test-data/canary/sagemaker'

session = sagemaker.Session()
ll = sagemaker.estimator.Estimator(container,
                                    'bee-roles-prod-us-east-1-DseDevSagemakerRole-ON6H1J6PJOXR', 
                                    train_instance_count=1, 
                                    train_instance_type='ml.m4.4xlarge',
                                    output_path='s3://{}/{}/output'.format(bucket, prefix),
                                    sagemaker_session=session)
ll.set_hyperparameters(
    feature_dim=len(train_data.columns)-1,
    mini_batch_size=500,
    predictor_type='regressor'
)
```

Now we'll create the input data by referencing the files we wrote to S3 when we split our training dataset:

```python
s3_input_train = sagemaker.s3_input(s3_data='s3://{}/{}/train/train.csv'.format(bucket, prefix), content_type='text/csv')
s3_input_validation = sagemaker.s3_input(s3_data='s3://{}/{}/validation/validation.csv'.format(bucket, prefix), content_type='text/csv')
```

And finally, we want to actually fit the model:


```python
job_name = 'canary-cpi-model-{timestamp}'.format(timestamp=int(time.time()))
ll.fit({'train': s3_input_train, 'validation': s3_input_validation}, job_name=job_name) 
```
    INFO:sagemaker:Creating training-job with name: canary-cpi-model-1553203494
    2019-03-21 21:24:55 Starting - Starting the training job...
    2019-03-21 21:24:56 Starting - Launching requested ML instances......
    2019-03-21 21:26:05 Starting - Preparing the instances for training...
    2019-03-21 21:26:53 Downloading - Downloading input data
    2019-03-21 21:26:53 Training - Downloading the training image....
    ...
    2019-03-21 21:28:01 Completed - Training job completed
    Billable seconds: 75

Now that we have a trained model, we want to determine how well the model performs.  We'll do this by running our test data through the model and comparing the results to the expected value.  

Let's start by deploying the model so we can score against it:


```python
ll_predictor = ll.deploy(initial_instance_count=1, instance_type='ml.m4.xlarge')
```
    INFO:sagemaker:Creating model with name: linear-learner-2019-03-21-21-28-38-494
    INFO:sagemaker:Creating endpoint with name canary-cpi-model-1553203494
    --------------------------------------------------------------------------------------!

We'll read in our test dataset and then setup our model to receive csv data:

```python
test_data = pd.read_pickle('./data/test-data.pkl')

ll_predictor.content_type = 'text/csv'
ll_predictor.serializer = csv_serializer
ll_predictor.deserializer = json_deserializer
```

Now we'll loop loop over our test dataset to:
* split data into mini-batches
* convert those batches into CSV payloads
* get predictions for each payload
* merge the result back into our test dataset
* calculate the MAE for our test dataset (this is the metric we will use to evaluate the model fit)


```python
def predict(data):
    predictions = []
    for array in data:
        result = ll_predictor.predict(array)
        predictions.append(result['predictions'][0]['score'])
    
    return np.array(predictions)

test_data['prediction'] = predict(test_data.drop(['conversion_rate'], axis=1).as_matrix())
test_data['error'] = np.abs(test_data['prediction'] - test_data['conversion_rate'])
print('mean average error: {error}'.format(error=test_data['error'].mean()))
```
    mean average error: 0.00058917052205

So a MAE of 0.0006 is VERY good. One other thing to look at is the error for rows with non-zero conversion rates since what we really care about is identifying inventory with good conversion rates. Let's try this by calculating the MAE for only rows that have a `conversion_rate` greater than 0:

```python
print('mean average error for non-zero conversion rate: {error}'.format(error=test_data.loc[test_data['conversion_rate'] > 0]['error'].mean()))
```
    mean average error for non-zero conversion rate: 0.179533322674

Okay, worse than overall but still pretty decent... we have reasonable but notably higher error for rows that actually have a conversion rate. What does this mean? It means we are really really good at predicting which inventory will not perform but not as good at predicting what will perform. Let's try to improve performance.

# Model Tuning
To combat the relatively small number of conversions, we can [upsample](http://www.simafore.com/blog/handling-unbalanced-data-machine-learning-models) the training set so that the conversions are more evenly balanced with the non-conversions. This will ultimately allow the model to train on a more evenly distributed dataset. Our goal is to create a balanced dataset for training, and then to test on an unbalanced dataset to make sure the model still works in the real world.

Let's start by re-loading our dataset from Step 2:
```python
df = pd.read_pickle("./data/step2-model.pkl")
```

Now let's do the sampling. We'll try to improve the ratio so that at least 5% of rows have some conversion rate.
```python
# 100% of the data where conversion_rate > 0
sampled_data = df.loc[df['conversion_rate'] > 0]

# percentage to sample
sample_rate = len(sampled_data) * 20.0 / (len(df) - len(sampled_data))
print('sample rate: {}'.format(sample_rate))

# finally, let's merge the two together
sampled_data = pd.concat([sampled_data, df.sample(frac=sample_rate)], axis=0, ignore_index=True).to_dense()
print('new data size: {}'.format(sampled_data.shape))
```
    sample rate: 0.0410933604211
    new data size: (1873, 449)

Okay, now we have a much better ratio of converters to non-converters, and the added benefit of a much smaller dataset that will allow us to move much faster from here out. This should give us a better fitting model. Let's find out by re-running our modeling process. We'll first need to re-generate our input datasets:
```python
train_data = sampled_data.sample(frac=.9)
validation_data = sampled_data.drop(train_data.index)

pd.concat([train_data['conversion_rate'], train_data.drop(['conversion_rate'], axis=1)], axis=1).to_csv('data/sampled/train.csv', index=False, header=False)
pd.concat([validation_data['conversion_rate'], validation_data.drop(['conversion_rate'], axis=1)], axis=1).to_csv('data/sampled/validation.csv', index=False, header=False)

boto3.Session().resource('s3').Bucket(bucket).Object(os.path.join(prefix, 'sampled/train/train.csv')).upload_file('data/sampled/train.csv')
boto3.Session().resource('s3').Bucket(bucket).Object(os.path.join(prefix, 'sampled/validation/validation.csv')).upload_file('data/sampled/validation.csv')

os.remove('data/sampled/train.csv')
os.remove('data/sampled/validation.csv')
```
and then re-fit our model:
```python
prefix = 'bid-models-test-data/canary/sagemaker/sampled'

session = sagemaker.Session()
ll = sagemaker.estimator.Estimator(container,
                                    'bee-roles-prod-us-east-1-DseDevSagemakerRole-ON6H1J6PJOXR', 
                                    train_instance_count=1, 
                                    train_instance_type='ml.m4.4xlarge',
                                    output_path='s3://{}/{}/output'.format(bucket, prefix),
                                    sagemaker_session=session)
ll.set_hyperparameters(
    feature_dim=len(sampled_data.columns)-1,
    mini_batch_size=200,
    predictor_type='regressor'
)

s3_input_train = sagemaker.s3_input(s3_data='s3://{}/{}/train/'.format(bucket, prefix), content_type='text/csv')
s3_input_validation = sagemaker.s3_input(s3_data='s3://{}/{}/validation/'.format(bucket, prefix), content_type='text/csv')

job_name = 'canary-cpi-model-sampled-{timestamp}'.format(timestamp=int(time.time()))
ll.fit({'train': s3_input_train}, job_name=job_name) 
```
    INFO:sagemaker:Creating training-job with name: canary-cpi-model-sampled-1553349917
    2019-03-23 14:05:17 Starting - Starting the training job...
    2019-03-23 14:05:19 Starting - Launching requested ML instances......
    2019-03-23 14:06:25 Starting - Preparing the instances for training...
    2019-03-23 14:07:12 Downloading - Downloading input data
    2019-03-23 14:07:12 Training - Downloading the training image.....
    2019-03-23 14:08:08 Uploading - Uploading generated training model
    2019-03-23 14:08:08 Completed - Training job completed
    Billable seconds: 64

Now let's evaluate the model as before. I'm going to use our original test dataset (without sampling) to make sure that our sampling didn't cause us to overfit the model.
```python

ll_predictor = ll.deploy(initial_instance_count=1, instance_type='ml.m4.xlarge')
ll_predictor.content_type = 'text/csv'
ll_predictor.serializer = csv_serializer
ll_predictor.deserializer = json_deserializer

test_data['prediction'] = predict(test_data.drop(['conversion_rate'], axis=1).as_matrix())
test_data['error'] = np.abs(test_data['prediction'] - test_data['conversion_rate'])

print('mean average error: {error}'.format(error=test_data['error'].mean()))
print('mean average error for non-zero conversion rate: {error}'.format(error=test_data.loc[test_data['conversion_rate'] > 0]['error'].mean()))
```
    INFO:sagemaker:Creating model with name: linear-learner-2019-03-23-14-08-29-349
    INFO:sagemaker:Creating endpoint with name canary-cpi-model-sampled-1553349917
    --------------------------------------------------------------------------!
    
    mean average error: 0.0136699411685
    mean average error for non-zero conversion rate: 0.120185396491


As expected, we've been able to balance our model a little better. We are now slightly worse at determining what does not perform well but better at determining what does perform well. At this point we could continue tuning our model by a) tuning the model's hyperparameters (the configuration for the model itself) and b) looking at different combinations of features to include or exclude from the model but these are outside the scope of this tutorial.  et's call the current version of our model "done" for now and save its metadata so we can access it later.
```python
features = list(sampled_data.columns)
features.remove('conversion_rate')
prod_model = {
    'features': features,
    'endpoint_name': job_name
}

with open('data/prod_model.json', 'w') as f:
    f.write(json.dumps(prod_model))
```

In [part 2](https://github.com/BeeswaxIO/beeswax-api/blob/master/beeswax/tutorials/bid_models_cpi/Part-2_Deploying-the-Model.md) of this tutorial, we'll upload our model to Beeswax and use it in a live campaign.

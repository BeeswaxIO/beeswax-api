# Introduction
Beeswax has recently released a feature called Bid Models, which allows customers to create a multi-variate model to determine the exact bid for any combination of variables available on a programatic bid request. The idea is that, as a Beeswax user, you can leverage your existing logs (auctions, bids, wins, conversions, etc) to build a model that predicts the likelihood of some metric such as a click-through or app install. That prediction can then be used to determine how much you should bid on each auction. In general Bid Models are meant to be flexible, allowing you to use any modeling tools/workflow and express the model in a straight forward format. A typical workflow might look like the following:

1. Create a model using Beeswax logs (wins, conversions, etc) and/or proprietary data.  Model features are bid request keys, and the prediction is either a bid or a bid multiplier.
2. Run a bunch of auction logs through the model to get a predicted bid price for each auction and create a set of prediction files from these predictions.
2. Create a Bid Model via [Beeswax's API](https://docs.beeswax.com) or UI, upload the predictions to Amazon S3, and tell Beeswax the location.
3. Attach the Bid Model to a campaign or line item.
4. When a bid request is made for that line item, Beeswax does a lookup against the Bid Model. If there is a match, that value is used as the bid or multiplier. If there is no match, the default bid is used.
5. As the campaign runs, use the performance data to retrain the model and upload new versions.

In this tutorial, we will go through these steps end-to-end, including building a machine learning model with RTB logs and deploying it as a Bid Model on Beeswax. I'm going to leverage [Amazon Sagemaker](https://aws.amazon.com/sagemaker/) and the popular Pandas python library to build my model. This will give me a Jupyter notebook environment managed by AWS with most of the networking and data access permissions I need.  That said, the techniques applied in this tutorial are pretty general and should apply to the modeling environment of your choice.  

Ultimately, we need to produce two assets in order to run our Bid Model on Beeswax:
* a "manifest" file that describes our model
* a set of "prediction" files that contain the actual data for our model.  The exact size and shape of these files will vary depending on your model but a simple example could look something like this:

| app_bundle | display_manager | placement_type   | banner_height | platform_os_version | value          |
|------------|-----------------|------------------|---------------|---------------------|----------------|
| 1005765746 | Fyber           | BANNER           | 320           | 4.1                 | [expected bid ]|
| 1008508212 | SOMA            | BANNER           | 320           | 11.0                | [expected bid ]|
| 1016562846 | AerservSDKiOS   | BANNER_AND_VIDEO | null          | 12.0                | [expected bid ]|
| ...        | ...             | ...              | ...           | ...                 | ...            |

For this exercise we are going to build a Cost-Per-Install (CPI) model, which will bid more on users who are more likely to download our mobile app. The purpose of this tutorial is not to go in-depth on CPI prediction so we are going to make some basic assumptions to simplify things:
* we will assume every install has the same value
* we will ignore auction dynamics like bid floors, market pricing, first vs second price etc
* our model will be general enough to use with any campaign, and not based on performance data from one particular campaign or set of creatives

We are going to use the following simple equation to calculate bid price:

>conversion_value * likelihood_of_conversion = bid_price

In this scenario, our "conversion event" is an app install, so our model will predict the likelihood that a particular auction will lead to an app download. We just need to know how much each install is worth to us and then we can calculate our bid. For the purpose of this exercise, let's assume that we've done some research and determined that the lifetime value of a single app install is $5 (our conversion value). In other words, our goal is to build a model that can achieve a CPI of <$5.

This tutorial has two parts:
* In [Part 1](https://github.com/BeeswaxIO/beeswax-api/blob/master/beeswax/tutorials/bid_models_cpi/Part-1_Building-a-Model.md), we discuss ingesting and preparing log data and then generate our CPI model using SageMaker
* In [Part 2](https://github.com/BeeswaxIO/beeswax-api/blob/master/beeswax/tutorials/bid_models_cpi/Part-2_Deploying-the-Model.md), we create a set of prediction files from our CPI model and then upload to Beeswax 

Full code for this tutorial can be found in the ["notebooks"](https://github.com/BeeswaxIO/beeswax-api/tree/master/beeswax/tutorials/bid_models_cpi/notebooks) folder in this repo.

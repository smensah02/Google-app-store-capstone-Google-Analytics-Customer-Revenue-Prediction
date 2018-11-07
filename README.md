# Google Store Predictive Analysis 
## A Kaggle Challenge 

## Project Description 
The 80/20 rule has proven true for many businesses–only a small percentage of customers produce most of the revenue. As such, marketing teams are challenged to make appropriate investments in promotional strategies.

RStudio, the developer of free and open tools for R and enterprise-ready products for teams to scale and share work, has partnered with Google Cloud and Kaggle to demonstrate the business impact that thorough data analysis can have.

In this competition, We are challenged to analyze a Google Merchandise Store (also known as GStore, where Google swag is sold) customer dataset to predict revenue per customer. Hopefully, the outcome will be more actionable operational changes and a better use of marketing budgets for those companies who choose to use data analysis on top of GA data. https://www.kaggle.com/c/ga-customer-revenue-prediction

## Problem Statement 
Predicting How Much a Customer Would Spend at a GStore. With such outcome, operational changes and a better use of marketing budgets can be made by those companies who choose to use data analysis.


## Data Source
The Data was provided by Kaggle. Data-size for training data set = 1,468,195 KB; Data-size for test data set = 1,315,279 KB; Data format = .csv; These contain the data necessary to make predictions for each fullVisitorId listed in sample_submission_v2.csv.
However, imbedded in a few of the columns are json scripts (objects). These had to pulled out for exploration then joined to the data frame. Within the total column (a json object) contained our label referred to as transactionRenue. This variable is what we use to predict on our testing data.

## Exploratory Data Analysis
I carefully examined each column closely and columns that had consistently the same value for each observation or didn't seem to place much relevance or had the same data present in another column were dropped. Such columns include:

['browserSize', 'browserVersion', 'flashVersion', 'language', 'mobileDeviceBranding', 'mobileDeviceInfo', 'mobileDeviceMarketingName', 'mobileDeviceModel', 'mobileInputSelector', 'operatingSystemVersion', 'screenColors', 'screenResolution', 'visits','adwordsClickInfo', 'campaignCode','socialEngagementType','networkLocation', 'longitude', 'latitude', 'cityId', 'metro', 'country', 'region', 'subContinent', 'isMobile', 'medium']


Filled all Nan's with -999 for categorical variables and numerical variables with 0. This was done because I did not want the categorical columns affected much when we get dummies on them turning them to 1s and 0s. Also the missing values in the numerical columns example transactionRevenue might hold the same relevance as the value 0, because in both cases we might say no transaction or actual sale was made when customer visited the site. We could say that the customer left the site without checking through the merchandise in the store or did not get to the store page.

For each column that has a json script imbeded, I transform them into a data frame. For example df['totals']. Once the column has been turned into a data frame. some more EDA is done by deleting columns that would play any effect on our model either because its the same for all rows or completely empty or has no value. After EDA, this column is added to the main data frame while the previous json column is dropped to avoid any duplicates. The total column is illustrated below.


## Models

First I began with a simple Linear Regression model using the totals dataframe (column). The result was a very poor score. 

`(~ 0.025320 for train, 0.027986  for test)`

Based on the perfomance of our model, we see that while there is a bit of underfitting going on, our score shows that we have quite a bit of room to improve on. A quick RMSE metric showed us how poorly our model was doing with an approximate score of `52.933 for training and 49.474 for testing`. For RMSE, the closer you are to 0 the better.

After trying a couple more models with both numerical and categorical variables, the best model that seem to perform the best so far was Extra Trees Regressor and Gradient Boosting Regressor with very little overfitting. The scores from gradient boosting was `(approximately 0.99993 for train and 0.99183 test data)` 

RMSE score for gradient boosting was approximately 0.417 for training and 4.533 for testing. A much better improvement from our first base model.

## Summary
- We began with trying to predict the how much customers will spend at a gStore.
- We analyze our data, performed some EDA and dropped the necessary columns.
- We tried predicting just on numerical columns and found that to be adequately lacking; we then tried predicting on all remaining columns, both numerical and categorical coloumns, and found that our model performed much better. 
- Though we are scoring at 99% on some of our models, we realize that there is still room for improvement.

## Take Away
> **We could potentially use this model to predict how much a customer will spend on any ecommerce store with similar data collection.**

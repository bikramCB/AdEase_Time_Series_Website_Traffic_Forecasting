# AdEase_Time_Series_Website_Traffic_Forecasting

## Business Model:
Ad Ease is an ads and marketing based company helping businesses elicit maximum clicks @ minimum cost.  AdEase is an ad infrastructure to help businesses promote themselves easily, effectively, and economically.
Suppose Nike wants to place an ad on any website through Social media platform like facebook, Instagram, If an user clickes on ad they have to pay 1$ , 0.8$  would come to Social media profile and 0.2$ would go to
Nike.

## Problem Statement:
Data Science team of Ad ease trying to understand the per page view report for different wikipedia pages for 550 days, and forecasting the number of views so that you can predict and optimize the ad placement for your clients. You are provided with the data of 145k wikipedia pages and daily view count for each of them. Your clients belong to different regions and need data on how their ads will perform on pages in different languages.

## Data:
There are two csv files given

train_1.csv: In the csv file, each row corresponds to a particular article and each column corresponds to a particular date. The values are the number of visits on that date.

The page name contains data in this format:

SPECIFIC NAME _ LANGUAGE.wikipedia.org _ ACCESS TYPE _ ACCESS ORIGIN

having information about the page name, the main domain, the device type used to access the page, and also the request origin(spider or browser agent)

Exog_Campaign_eng: This file contains data for the dates which had a campaign or significant event that could affect the views for that day. The data is just for pages in English.

There’s 1 for dates with campaigns and 0 for remaining dates. It is to be treated as an exogenous variable for models when training and forecasting data for pages in English.

## Tech Used:
ARIMA, SARIMAX, Prophet and Linear Regression

## Tools used:
Numpy, pandas, statsmodel,fbprophet

## Findings :
1.  there are some null values at the beginning probable reason website were not created at that time.
2. remove columns whose have more than 300 days views are null because its nonsense to predict 550 days forecast with 330 days 0 values.
3. every website name contains title, language,britanica.org,access type and access origin. split all title, language , access type and access origin.
4.  Then we took the mean views of every languages of 550 days(july 2015 to December 2016) each consider as views per page.
5.  English has the highest number of views per page.Did not remove spike outlier just becasue of there may be some significant incident happened thats why views were higher.

## Challenges:
Buring spliiting of title name, language from website we noticed some websites are unstructed way .Could not able to split title, language, access type. That why we consider them as no langugae or common language.

## Model:
As we have English language with the highest number of views and only have exogeneous variable for English language. So we did only forecast for english website. But this model is suitable for other languages too.
1. Remove trend and seasonality make the data stationary.
2. Then apply ARIMA model with p,d,q = 4,1,3 (hyperparameter tuning) with MAPE score of 0..093
3. Apply SARIMAX model with exogeneous variable to forecast last 30 days with training first 520 days and got MAPE score of 0.047
4. Apply Prophet method  to calculate MAPE score of 0.065
5. Apply Linear Regression: create a addition feature 'day of week' along with eng mean views and particular date column, exogeneous date. Do encoding of the dataframe of day of week.take rolling mean avg of 7 days, split traing and test data and make forecast of last 30 days with 520 days training data and calculate MAPE of 0.045.

## Business Impact:
This model help AdEase for client engaging to place their ad placement in proper way. Ans this way they generate 6-7% revenue this next year.

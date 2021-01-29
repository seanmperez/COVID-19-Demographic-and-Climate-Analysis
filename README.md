# What Drives COVID-19 Infection Rates, and Can We *Predict* It?

This project leverages public census data, weather data, and COVID-19 data on over 3,000 US counties to gain *inference* on the most important features correlated with COVID-19 rates, and uses those features to create a *predictive model* that may prove useful in future pandemics.  

# Motivation

The year 2020 is one we may never forget. The COVID-19 epidemic has taken away our favorite hobbies, quality of life, and perhaps even our loved ones. This has left us with so many questions, and luckily, there is so much data out there to better understand what happened.

I find data comforting in this time of distress, so I sought out what types of questions can be answered given public data available. With the start of a new year, there are a few things I'm especially concerned about with Coronavirus:

1. The plummeting temperatures in the New Year
2. Growing inequality across the United States

Below is my analysis to answer the question:

_**What demographic and weather features are the most important drivers to COVID-19 infection rates among US counties**?_

and

_**Can we use these  features to predict infections rates among counties?**_

# Data

All of this data is public and some are held in massive databases. But not to worry! I provide functions that download, process, and load the census, weather, and covid data in a memory efficient manner with parameter wiggle room to suit your needs! 

The raw data comes from 3 sources:

### 1. Census

The American Community Survey (ACS) provides yearly estimates as opposed to the US Census that provides data every 10 years, making it a much more useful tool since only the 2010 US Census is currently available. 

The ACS 1-year, and ACS 5-year 2019 estimates contain US county level data on race, ethnicity, insurance rates, and economic characteristics from the [Census Bureau APIs](https://www.census.gov/data/developers.html).

The ACS 1-year data provides the most current estimates, but also has the lowest coverage. This will be useful for inference, but not for predictive modeling.

![Alt text](https://github.com/seanmperez/COVID-19-Demographic-and-Climate-Analysis/blob/main/Figures/Counties_2019_ACS1_Census.png)

The ACS 5-year data provides the least current estimates, but has *great* coverage! This will be our go to for predictive modeling. 

### 2. Climate (temperature and precipitation)

The daily Global Historical Climatology Network (GHCN) [dataset](https://www.ncdc.noaa.gov/ghcn-daily-description) contains climate data (including temperature and precipitation) across 100,000 stations. The station metadata provides that latitude and longitutude. 

This data has little coverage, and has a slight bias since most stations are in the West. 
![Alt text](https://github.com/seanmperez/COVID-19-Demographic-and-Climate-Analysis/blob/main/Figures/Counties_2019_Weather.png)

In order to use this data for our predictive models, we will have to do some data imputation for missing counties.

### 3. COVID-19 

The Johns Hopkins University Center for Systems Science and Engineering COVID-19 [dataset](https://github.com/CSSEGISandData/COVID-19) contains global daily COVID-19 metrics at the County level for US data. This dataset also has a key for US County names with their respective [FIPS codes](https://github.com/CSSEGISandData/COVID-19).

This dataset has near complete coverage which is great since it will be used for both inference and prediction and contains our target metric, incidence rate.
![Alt text](https://github.com/seanmperez/COVID-19-Demographic-and-Climate-Analysis/blob/main/Figures/Counties_2019_COVID19.png)


### Merging the data

In order to merge data these disparate data sources we need a common key. Luckily the census and covid datasets have this key, FIPS codes. The weather dataset does not, so we need reverse geocode the latitude longitutde to extract the FIPS code region each weather station is in. Enough words, here is the schema below:

![Alt text](https://github.com/seanmperez/COVID-19-Demographic-and-Climate-Analysis/blob/main/Figures/data_schema.png)

# Results

### Inference

For inference, I use linear regression since it allows us to easily assess the direction and weight of each feature making it more intepretable than other algorithms. In order to interpret the significance of the features, I use Ordinary Least Squares hypothesis testing, as well as two types of regularization techniques, Ridge and LASSO regression. Regularization prevents models from overfitting by shrinking the size of the coefficients through an penalization term which is weighted by a hyperparameter, alpha. Whew, that's a mouthful!

Since linear regression is a parametric model, transforming our features closer to a normal distribution is a key to success! 

_insert image of raw distribution_

_insert image of transformed distribution_

After feature transformation we need to normalize our features 

For our regularization models, we need to choose a hyperparameter alpha.

We can visualize the effect of different alphas on the weight of each coefficient.

_insert two images of alpha vs coefficients_

We can then use cross validation to choose the optimal alpha, build each model, and view a heatmap of the coefficients.

_insert heatmap_


### Predictive Models

# Acknowledgements

There are quite a few people/articles I'd like to thank for inspiration.

1. **Francisco Utrera** - Spent many a night discussing experimental design and feature transformations over tea.
2. **Data 100** - This class final project was the starting point of this analaysis and provided a few basic functions to download the weather data. The class also went into great depth of the linear algebra and loss functions behind common machine learning algorithms!
3. **Articles** - What would we do without asking the internet for help?
  - https://www.analyticsvidhya.com/blog/2020/04/feature-scaling-machine-learning-normalization-standardization/
  - https://towardsdatascience.com/getting-census-data-in-5-easy-steps-a08eeb63995d
  - https://www.kdnuggets.com/2017/10/xgboost-concise-technical-overview.html
  -

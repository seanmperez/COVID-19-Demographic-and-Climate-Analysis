# What Drives COVID-19 Infection Rates, and can we Predict it?

This project leverages public census data, weather data, and COVID-19 data on over 3,000 US counties to gain *inference* on the most important features correlated with COVID-19 rates, and uses those features to create a *predictive model* that may prove useful in future pandemics.  

# Motivation

The year 2020 is one we may never forget. The COVID-19 epidemic has taken away our favorite hobbies, way of life, and perhaps even our loved ones. This has left us with so many questions, and luckily, there is so much data out there to better understand just what happened.

I find data comforting in this time of distress, so I sought out what types of questions can be answered given public data available. With the start of a new year, there are a few things I'm especially concerned about with Coronavirus:

1. The plummeting temperatures in the New Year
2. Growing inequality across the United States

Below is my analysis to answer the question **What weather and demographic features are the most important drivers to COVID-19 infection rates**?

# Data

All of this data is public and some are held in massive databases. No worries as I provide functions that download, process, and load the census data, weather data, and covid data in a memory efficient manner with parameter wiggle room to suite your needs! 

The raw data comes from 3 sources:

### 1. Census
The ACS 1-year, and ACS 5-year 2019 estimates contain US county level data on race, ethnicity, insurance rates, and economic characteristics from the [Census Bureau APIs](https://www.census.gov/data/developers.html).


### 2. Climate (temperature and precipitation)
The daily Global Historical Climatology Network (GHCN) dataset contains global daily climate data (including temperature and precipitation) across 100,000 stations (read more here: https://www.ncdc.noaa.gov/ghcn-daily-description). The stations metadata provides that latitude and longitutude. 


### 3. COVID-19 
The Johns Hopkins University Center for Systems Science and Engineering COVID-19 dataset contains global daily COVID-19 metrics at the County level for US data (read more here: https://github.com/CSSEGISandData/COVID-19). This dataset also has a key for US County names with their respective FIPS codes also found in the Johns Hopkins University Center for Systems Science and Engineering [github repo](https://github.com/CSSEGISandData/COVID-19).

# Results

# Inference

# Predictive Models

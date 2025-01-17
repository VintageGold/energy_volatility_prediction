# Energy Volatility Prediction
## UMBC Fall 2021 Data Science Capstone

### Abstract
Our project aims to understand the volatility of electricity prices across the U.S. aggregated by state and years 2001-2020 across features encompassing fuel sources (MWh and powerplant count), fuel consumption by residential, commercial, and industrial sectors (normalized by state population and number of electric accounts), weather (temperature and drought index), and historical futures contracts (open, high, low, close, and volume for Crude Oil, Natural Gas, and Heating Oil futures contracts) to explore this question. Our target variable is the coefficient of variation in electricity price. The model that best explains our target variable is an XGBoost Regressor model. This model achieved an adjusted R2 of 0.77 and heavily relies on the coefficient of variation of the previous year, state, the Brents Crude Oil futures contract data, and features that reflect the supply and demand of electricity (ex. Total plant count). This model performs consistently, with exceptions to LA, OK, RI, and HI. A particular anomaly is NV which trains well, but struggles with the test data.

### Instructions for use:
1. We have a data folder saved on our google drive as a shared drive. This contains the data gathered and processed in the notebooks found in this repository.
  a. Permission is required to access this folder (our professor has permission).
2. Open google colab and clone this repository into the environment.
3. Run the code of any notebook you desire- if asked to mount your drive, select the email address we have shared the drive with, and copy and paste the link.
4. Since the shared folder should show up as part of your shared drive at the user end, the folder paths should all work.

## Repository Contents
---
<pre>
Data Notebooks           : <a href=https://github.com/harperd17/energy_volatility_prediction/tree/main/notebooks/Data%20Ingestion>Data Ingestion </a>
                         Here is where data is ingested and aggregated to meet the format of one row per year and state.
                         : <a href=https://github.com/harperd17/energy_volatility_prediction/tree/main/notebooks/Data%20Filling>Data Filling </a>
                         Here is where we filled in missing years of electric accounts data using regression. 
                         : <a href=https://github.com/harperd17/energy_volatility_prediction/tree/main/notebooks/Validation>Data Validation </a>
                         Here is where we do validation of the plant and energy source data.

EDA Notebooks            : <a href=https://github.com/harperd17/energy_volatility_prediction/tree/main/notebooks/EDA>EDA </a>
                         Here is where we have our notebooks for EDA. This includes basic EDA and EDA that explores the relationships of different variables to the target                              variable.
                         
Modeling Notebooks       : <a href=https://github.com/harperd17/energy_volatility_prediction/tree/main/notebooks/Modeling>Modeling </a>
                         Here is where all our modeling notebooks are stored. We have one notebook for decision tree classifier, one for linear regression, another for XGB                            regression, and lastly, a notebook where we explore all types of models using the neptune logging functionality.
                
Slide Decks              : <a href=https://github.com/harperd17/energy_volatility_prediction/tree/main/powerpoints>Powerpoints </a>
                         Our phase 1, 2, and 3 slide decks can be found here.

Helper Function Files    : <a href=https://github.com/harperd17/energy_volatility_prediction/tree/main/helpers>Helper Functions </a>
                         Commonly used functions are stored in files across this folder and used throughout our project.
</pre>


# Data: 2001-2020

##  Electricity Price
We have monthly electricity price data by state. The average and standard deviation price was calculated for each state for each year which were used to calculated the coefficient of variation as such: (standard deviation of price across all months in a year) / (mean price across all months in a year).<br>
## Electricity Consumption<br>
We have historical monthly electricity consumption based on sectors (COM, IND, and RES).  Which are aggregated to an annual level and measured in kWh.<br>
## Powerplant<br>
We have historical monthly electricity net generation data from each plant in the United States. Which are aggregated to an annual level and measured in MWh.<br>
## Weather<br>
We have monthly historical temperatures and palmer drought severity index values (pdsi) across the US gridded at a 60km x 60km resolution. Data from 1981 to 2000 was used to calculate averages and standard deviations from each of these locations. These were used to standardize the data for our years of interest (2001-2020). This data is aggregated to a state level. Currently, we are using three derived terms; number of summer months with temperatures above 1 standard deviation above the mean, number of winter months with temperatures below 1 standard deviation below the mean, and number of months with a pdsi value lower than 1 standard deviation below the mean (the lower the pdsi, the worse the drought).<br>
## Futures Contracts<br>
We started with daily open, high, low, close, and volume for the following futures contracts; NG (natural gas), CL (crude oil), BZ (brent crude oil), and HO (heating oil). Daily price movement was derived as the difference between the high and low price for each day. A moving average and standard deviation of the price movement and volume was used to standardize these variables. For each year and futures symbol, the total number of days with above average price movement and volume is calculated (the current names of these variables is misleading and should be changed).<br>

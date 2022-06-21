# Practicum-Project: 
### Main Greenhouse Gas Contributors and Future Emission Predictions
 My goal in this practicum project is to determine the main contributors to greenhouse gas emissions and make future emission predictions. Climate change is a very real crisis we are facing today and human emissions of co2 and other greenhouse gases are a primary driver of climate change. I would like to dig deeper into this and determine what specifically is playing a role in these increased emissions and predict how these rates will change in years to come.

I will be implementing various machine learning techniques such as Random Forest Regression, KNN Imputation for missing values, and ARIMA time series forcasting for predicting future emission values. 

##### Keywords: 
Random Forest Regression, Knn Imputation, ARIMA time series forcasting


# Table of Contents
1. Dataset Description
2. Exploratory Data Analysis and Feature Importance
3. Handling Missing Data
4. Analysis
5. Findings
6. Future Steps


# Dataset Description
1. The first dataset I used consisted of yearly emission values from the late 1700s to 2020 for 248 countries/regions and includes the world. Some emission values included co2, methane, nitrous oxide. There are three datatypes in this dataset: Float which included all emission values, Int which represented the year of observation, and Categorical which represented the country/region where the observation took place. The original dataframe size was 60 columns and 25,989 rows, after cleaning the dataset and removing unnecessary columns, the dataframe size was 44 columns and 25,989 rows. 
#### See https://github.com/owid/co2-data/blob/master/owid-co2-codebook.csv for a full dataset description from Our World in Data

2. The second dataset I used was from the World Recources Institute and includes a breakdown of global emissions by sector from the year 2020. I used this dataset because it is important for us to know where these emissions are coming from in order to reduce our emissions. 

# Exploratory Data Analysis and Feature Importance
#### Using Pearsons Correlation where target column is co2
1. 10 most positively correlated columns to co2
![Screenshot 2022-06-21 102846](https://user-images.githubusercontent.com/95181908/174900185-5c53e553-ebaf-484a-9b39-ab3102c38337.png)
2. 10 most negatively correlated columns to co2
![Screenshot 2022-06-21 152548](https://user-images.githubusercontent.com/95181908/174900288-7670d7d9-d21c-4b56-bf15-2c3bc8c9698f.png)

#### Using Random Forest Regression to determine feature importance for co2 column
![Screenshot 2022-06-21 103145](https://user-images.githubusercontent.com/95181908/174900432-27f9eab3-3941-45b9-b991-32449caf3bca.png)


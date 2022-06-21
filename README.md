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
##### Correlation Heatmap Plots
1. 10 most positively correlated columns to co2
![Screenshot 2022-06-21 102846](https://user-images.githubusercontent.com/95181908/174900185-5c53e553-ebaf-484a-9b39-ab3102c38337.png)
From the figure above we can see that our most posititvely correlated columns to our co2 column are 'oil_co2', ''cummulative_coal_co2', 'gas_co2', 'gdp', 'primary_energy_consumption', ''coal_co2', 'cumulative_gas_co2', and 'cumulative_oil_co2'.

2. 10 most negatively correlated columns to co2
![Screenshot 2022-06-21 152548](https://user-images.githubusercontent.com/95181908/174900288-7670d7d9-d21c-4b56-bf15-2c3bc8c9698f.png)
From the figure above, we cna see that our most negatively correlated columns to our co2 column are 'share_global_cumulative_gas_co2', 'total_ghg_excluding_lucf', and 'co2_per_unit_energy'.

#### Using Random Forest Regression to determine feature importance for co2 column
![Screenshot 2022-06-21 103145](https://user-images.githubusercontent.com/95181908/174900432-27f9eab3-3941-45b9-b991-32449caf3bca.png)
Lets graph this out to make it easier to view
![Screenshot 2022-06-21 155552](https://user-images.githubusercontent.com/95181908/174903900-a2f5e587-b616-4ff0-a109-8b1d6d4a64d3.png)
From the graph we can confirm that 'oil_co2' has the highest feature importance.

# Handling Missing Data
The amin dataset I used, the emissions dataset, had alot of missing data in it. 
##### The figure below represents the percent missing in each column.
![Screenshot 2022-06-21 160110](https://user-images.githubusercontent.com/95181908/174904472-73d640ff-ec9f-4752-8b59-049a68fd6198.png)
As we can see, a lot of columns have over 50% of their data missing.
My first step to handling the missing data was to drop all columns missing over 80% of their data. These columns that were dropped included 'trade_co2', 'flaring_co2', 'flaring_co2_per_capita', 'other_industry_co2', 'other_co2_per_capita', 'consumption_co2', 'consumption_co2_per_capita', 'consumption_co2_per_gdp', 'cumulative_flaring_co2', 'cumulative_other_co2', 'trade_co2_share', 'share_global_flaring_co2', 'share_global_other_co2', 'share_global_cumulative_flaring_co2', and 'share_global_cumulative_other_co2'. I also dropped the 'iso_code' column because I didn't believe that it was necessary for analysis because it represented a code for the region we were looking at. 
To handle the rest of the missing data, I scaled my data and made a KNN Imputer function to fill in the remaining null values. I separated the dataset into subsets grouped by the country column, this ensured that the missing values for that country/region were filled in based on other values for the region, and then ran the subsets through the KNN imputer function I created. 

# Analysis
1. One goal of my project was to understand where emissions were coming from. This is where my emissions by sector dataset came in. The figure below was created by using my second dataset and shows what percentage of global greenhouse gas emissions are created from which production sectors. 
![Screenshot 2022-06-21 125558](https://user-images.githubusercontent.com/95181908/174905669-a4aa7612-f466-4273-a32b-fcd1c1accaad.png)
I then further categorized the data into one of the following subsectors: 'energy', 'industry', 'Agriculture, forest, and land use' or 'waste'. The figure below shows this.
![Screenshot 2022-06-21 125641](https://user-images.githubusercontent.com/95181908/174905875-cfc9e7f5-312c-45c2-93cf-4bdd01cbf468.png)
We can see from the figure above that 73.2% of all greenhouse gas emissions are from energy production, 18.4% are form Agriculture, forest, and land use production, 5.2% are from industry production, and 3.2% are form waste production.

2. Since my first dataset listed at the beginning only included emission prediction up tto the year 2020, one goal of my project was to create future co2 emission predictions for years 2021-2026. To do this, I used the ARIMA time series prediction method. My first step here was to convert my 'year' categry form an integer value to a datetime value and make this the index of my dataset. 

 Next, I needed to check for stationarity in my co2 column. The figure below shows that our data was not stationary because mean is increasing even though the std is small, and Test stat is > critical value.
![Screenshot 2022-06-21 163216](https://user-images.githubusercontent.com/95181908/174907742-7c45d211-70bc-488e-9a31-7f77d1290406.png)

Since the data is not stationary, I used a ARIMA(1, 1, 0) model for my predictions. The four figures below are the results from fitting the ARIMA model.
![Screenshot 2022-06-21 112339](https://user-images.githubusercontent.com/95181908/174908073-d081ce6d-8846-4209-a823-10e643e1c9b2.png)
![Screenshot 2022-06-21 112354](https://user-images.githubusercontent.com/95181908/174908091-abd30118-f8b2-4b4f-ac1c-10e8e7cf7c37.png)
The plot above is showing a line plot of the residual errors. The results hsow a slight bias in the prediction (a non-zero mean in the residuals)
![Screenshot 2022-06-21 112411](https://user-images.githubusercontent.com/95181908/174908105-f9d66a20-097e-4218-af67-0edcf01d76ef.png)
the plot above shows that our errors are guassian and may be centeres at 0.
![Screenshot 2022-06-21 112423](https://user-images.githubusercontent.com/95181908/174908145-2b7503c0-6675-410c-b39e-351fd21f1ef1.png)

I ran a subset of the data (grouped by country) through the model to fit it and the figure below shows the expected co2 vlaue from the dataset in blue and the predicted value from the model in red. The figure is only for the 'World' country.
![Screenshot 2022-06-21 163840](https://user-images.githubusercontent.com/95181908/174908601-91789050-f551-4e51-ae7a-23f4d940ef41.png)
We can see form the above figure that the model did pretty well at predicting values.

# Findings
Lastly, I used the model to make co2 predictions for the years 2021-2026 for each country. I then added those predictions into the original dataframe and printed the original values and the future predicted values. The figure below represents our 'World' subset and the original values are shown in blue while the prediction values for years 2021-2026 are shown in red.
![Screenshot 2022-06-21 115144](https://user-images.githubusercontent.com/95181908/174908960-d933016c-6927-482a-8de0-a48f1221d53e.png)

# Future Steps
If I were to continue to do analysis with this project, my next steps would be
1. Complete ARIMA time series predictions for years 2021-2026 on ‘cement_co2', 'coal_co2', 'gas_co2', 'oil_co2', 'nitrous_oxide', and 'methane' columns.
2. Compare predicted results with actual values as the years go on.
3. Discover solutions to reduce emission rates.


# Weather Prediction at SF Airport

## Project Overview
This project aims to predict the weather at the San Francisco Airport using historical weather data. The main goal is to use machine learning techniques to predict various weather conditions such as precipitation, maximum temperature, and minimum temperature.

## Dataset
The dataset used in this project is `SF_Airport_Weather.csv`, which contains historical weather data from 1950 to 2023. The dataset includes 44 columns and 26964 rows. Each row represents a day's weather data. 

The data was obtained from the National Centers for Environmental Information (NCEI) website. Detailed documentation about the dataset can be found at the GHCND Documentation.

<ins> Links </ins>
https://www.ncdc.noaa.gov/cdo-web/search (Dataset Source)
https://www.ncei.noaa.gov/data/daily-summaries/doc/GHCND_documentation.pdf (Dataset Documentation)

## Data Preprocessing
The initial dataset contained many missing values. The percentage of missing values for each column was calculated. Based on this information, five core weather data columns were selected: "PRCP", "SNOW", "SNWD", "TMAX", "TMIN". These columns were renamed to "Precip", "Snow", "Snow_Depth", "Temp_Max", "Temp_Min" respectively for better readability.

It was observed that the 'Snow' column had a significant number of zero values and only one non-zero value (1.5). This skewness was taken into account during the model building process.

The 'Snow' and 'Snow_Depth' columns were dropped from the dataset as they were not needed. The date '2023-10-28' was dropped because all data for this date was NULL.

Missing values in 'Temp_Max' and 'Temp_Min' were filled using forward fill method (`ffill`). After these preprocessing steps, there were no missing values in the dataset.

The index of the DataFrame was converted to datetime format for further processing.

Additional features such as 'Year', 'Month', 'Day', 'Day_of_Year', 'Week_of_Year', 'Quarter', 'Day_of_Week', 'Is_Weekend', 'Is_Start_Month', and 'Is_End_Month' were created based on the date index.

An average temperature feature ('Temp_Avg') was created by taking the average of maximum and minimum temperatures.

A target variable was created by shifting the maximum temperature ('Temp_Max') by one day. The last row of the dataset was dropped since it had a null target value.

New features such as 'Month_Max' (30-day rolling mean of maximum temperature), 'Month_Day_Max' (ratio of monthly average temperature to daily maximum temperature), and 'Max_Min' (ratio of maximum to minimum temperature) were created.

A new feature, 'Monthly_avg', was created which represents the expanding mean of maximum temperature grouped by month. Another feature, 'Day_of_Year_avg', represents the expanding mean of maximum temperature grouped by day of year.

## Data Visualization
A plot of 'Temp_Max' and 'Temp_Min' against 'DATE' was created to visualize the temperature trends over time. Additionally, plots of average temperature ('Temp_Avg') and total precipitation ('Precip') resampled annually, monthly, quarterly, and weekly were also created to understand their trends over time.

## Model Building and Evaluation
A Ridge regression model was trained using predictors such as precipitation, maximum temperature, minimum temperature, monthly maximum temperature, ratio of monthly average to daily maximum temperature, ratio of maximum to minimum temperature, day of year average temperature, and monthly average temperature. The model was trained on data up to December 31, 2021, and tested on data from January 1, 2022 onwards.

The mean absolute error (MAE) of the model predictions on the test set was found to be approximately 3.30 degrees. This means that on average, the model's predictions are off by about 3.30 degrees.

The actual vs predicted temperatures along with their absolute differences were plotted for visualization. The top five predictions with highest differences and lowest differences were also displayed.

## Conclusion
The Ridge regression model performed reasonably well in predicting the maximum daily temperature at San Francisco Airport with an average error of about 3.30 degrees. The model could be further improved by engineering more relevant features or tuning hyperparameters.

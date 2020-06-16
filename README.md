# Beijing_AirQuality_Analysis_Project
_(Rutgers Student please use this project as a reference for your class only to avoid violate academic integrity)_
# Set up
* __import pandas as pd__
* __import numpy as np__ 
* __import matplotlib.pyplot as plt__ 
* __%matplotinline__
* __import seaborn as sns__
* __import altair as alt__

Please also add this line below: 
__alt.data_transformers.enable('data_server')__ 

Windows User please add this line: 
__alt.data_transformers.enable('default', max_rows=None)__

# Data Cleaning Process: 
In all four csv file, they all contain the same columns and the same number of rows but with different data. But we find there are missing values in each of the datasets. We want to find the best way we can do fill these missing values and avoid biases. In the end, we decided to fill the missing value by the average of the same cell from the other three datasets we choose. After we did that, we find out there are still about 200 rows with missing values, and we decide to drop these 200 rows. df_clean dataframe is the dataframe we're going to work on for the rest of the analysis. Please refer to the code above for more details.
# Data Format Desription: 
There are 15 columns in this dataset. There are year,month,day,hour as time in four different columns. And there greenhouses gases in columns, this includes PM2.5, PM10,S02,NO2,CO,03. And there are also columns like Temperature, Pressure, Dew Point Temperature, Rain and wind speed that could have affected or be affected by the greenhouse gases in the air. I believe all these columns are relevant in this data analysis because they all could have some kind of relationship with each other.

# Data Visualization: 
## Part 1: 
We are interested in the relationship between PM2.5 and PM10 base on the years, so we decided to do scatter plot and use year variable to distinguish the point.

As we can see from the above scatterplot that every year the PM2.5 and PM10 presented a linear relationship, and the linear regression line has been around 1:1 ratio for each year.

By definition, PM2.5 is particulate matter less than 2.5 micrometers, and PM10 is particulate matter less than 10 micrometers. Thus, we believe that most of the PM10 pollutants are from PM2.5. Since from the previous parts, we know that the average of PM2.5 is 79.58 ug/m^3 and the average of PM10 is 104.27 ug/m^3. We conclude that 80% of the PM10 pollutants are less than 2.5 micrometers.

We do notice there are some outliers where PM2.5 is higher than PM10. We think it is due to errors in the Dataset.

Definitions of PM2.5 and PM10 are from http://www.npi.gov.au/resource/particulate-matter-pm10-and-pm25

## Part 2: 
We are also interested in how the temperature could affect the density of the O3, so we decide to do a heat map to better visualize the data in this relationship.

According to the heatmap above, we're able to see that the density of O3 is usually less than 100 ug/m^3 when the temperature is less than 10 degrees Celsius. Once the temperature rises higher than 10 degrees Celsius, the O3/temperature ratio starts to increase exponentially. Thus, we conclude that there is an exponential relationship between Temperature and O3.

Definition of O3 is from https://www.environment.gov.au/protection/publications/factsheet-ground-level-ozone-o3

## Part 3:
We're interested in why CO density is much higher compare to other greenhouse gases, we believe it's because Beijing City is burning coal to supply heat to the city during the winter, we would like to do a line chart with confidence interval to see if there is a potential trend in the increase during winter months and observe its confidence interval changes throughout different months.

This line chart with confidence interval confirms our theory on the CO increases in the air. We can see there is a one times increase in CO density from October to December, and we believe it's because of burning coal to supply heat. Beijing city didn't change its heat supply source to natural gas until 2017. We also find out that the confidence interval for February is quite big compare to other months, we believe it's because the weather is not steady during this month, usage heat varies during the month.

## Part 4: 
We also want to find out the relationship between O3, wind speed, and rain. O3 is formed when nitrogen oxides (pollutants emitted from motor vehicles) react with sunlight. We believe that wind would blow the particles away from the urban area in Beijing to other places, which results in less O3 in the urban area. We also believe that rain could be a major factor, because the heavy cloud would block sunlight and halt the formation of ozone. We decide to do two cluster barchart to show this relationship.

From the above clustered bar chart, there is a correlation between wind speed and the concentration of O3. In June, July, and August, as the wind speed becomes lower, the concentration of O3 becomes higher.

We can also see that non-raining day mostly has high O3 density. The difference can be as great as 30% in July. Thus, we conclude that there is a relationship between rain and the concentration of O3.

## Part 5: 
We want to finally see a trend in each greenhouse gas density groupby hours. In that case, we can have a general idea on how each greenhouse gas's relationship with each other. This will prepare us a general sense on the future machine learning technique we're going to apply, clustering.

We're able to see a significant change in CO change base on hours, and other gas type are way at the bottom. Accrding to this chart, we can't really say only CO and O3 have effect on the clustering because these two curves are not as flat as the other, we need to further apply machine learning technique to see how the clustering works.

## Part 6: 
At the same time, we discovered the reason
behind the high wind speed and the high O3
density in May. It is because the average
temperature rises above 15 degrees, and
therefore people start to use AC.

Our conclusion that “the rain will wash the
particles away” still holds, because the density
of O3 is always lower during raining days.

# Machine Learning (K-Mean Clustering) 
We're going to sample our data from our new dataframe and do k-mean clustering between CO and 03 because according to the graph above, those two greenhouse gases has the bigger movement throughout time compare to other greenhouse gases.

From the above graph, we're able to easily identiy three clusters base on the relationship between CO and O3. And also from the previous graph, we can clearly see the inverse relationship between three graph.

In the last part we're going to do a Principal Component Analysis to analysis greenhouse gases and its effect on the temperature.

From the above graph and ratio, we can see that 67% of the variance is contributed by Principal Component 1 and 24% percent of the variance is contributed by Principal Component 2. And from the above graph,we're not able to clearly see the clusters in the graph, that is a indication that there is no relationship between Temperature and those greenhouse gases.

# Airbnb


## Introduction

Airbnb is an online platform that helps individuals connect who wants to rent their homes to the one
searching for accommodation. It presently encompasses more than 81,000 cities worldwide and 220
countries. The total number of listings worldwide is about 6 million and actively supports an average
of 2 million overnight stays (Zhu, et al., 2020).

To captivate more guests, the host has to provide a detailed description of his property. One of the
strategies to attract more tenants includes a reasonable price. The star rating system is usually used
for determining the cost of the property; currently, there are no clear price recommendations
available (Li, et al., 2016; Zhu et al., 2020).

# Research Question.

This study aims to analyze the Airbnb listing data and find the most relevant features that can be
used to suggest an ideal price to the host while listing a new property.

## Data Description.

Publicly available Airbnb data for New York city (Anon., n.d.) has been used for analysis. Variables
that are irrelevant to the study have been excluded from the data set. The data set has 59 columns
and 36,922 observations.

## Data Cleaning and Preprocessing.

The following steps are performed for data cleaning

```
 Reading 'listing.csv' to spark data Frame.
 Extracting only the features that the host will enter while listing a new property.
 Dropping rows with 'null' values in the 'host_since' column.
 Replacing the null values in the 'bedroom' column with the average number of
bedrooms.
 Replacing the null values in the 'beds' column with the average number of beds.
 Changing data type of columns' bedrooms’ and ‘beds’ to an integer.
 Parsing the values in ‘host_since’ as python’s DateTime objects.
 Counting the number of verifications each host has.
```

## Data Visualization.

Data visualization helps us get insights in the data and gives us the visual userstanding of the relation
between various data features. This section is one of the essential part in deciding the approach
towards the solution of the problem.

Figure 1 shows the data grouped by the month of registration & the mean price of the

### property:

![Figure 1](https://github.com/Rajas-Bakshi/Airbnb/blob/main/images/1.PNG?raw=true)

Observation: The plot above for counts (Numbers of registrations) is slightly skewed towards the
right i.e., more properties have been registered in the second half of the year. However, there is no
evident effect of the month of registration on the price of the property


The plot below (figure 2) shows the relationship between number of registrations each day of a
month & the mean price of the property.

```
Figure 2
```
Observation: No significant relationship can be observed between the date of registration and the
price of the property.

Plotting relations between the year of registration and number of registrations along with the
price of the property in figure 3.

```
Figure 3
```

Observation: Although there are more registrations from 2012 to 2017, no significant difference can
be seen in the property's price.

Thus, after analyzing the date of registration, it shows no significant effect on property price.

Understanding the types of properties that are majorly listed over the years, by plotting the
data on a pie chart in figure 4:

```
Figure 4
```
Observation: A large number of “Entire Home/apt” room type is listed over the years, followed by
“Private room”.

Plotting a pie chart of room type and the mean price for that room type to indicate the relation
between room type and price of the property are shown in figure 5:

```
Figure 5
```

Observation: The distribution in the mean price can be seen concerning the type of room. Although
the Entire Home/apt has the highest number of registrations, the hotel room has the highest mean
price.

Analyzing the relation between the number of beds and the count of properties along with its
cost in figure 6 and 7:

```
Figure 6 Figure 7
```
Figure 6 is a Graph for number of beds vs the count of properties and figure 7 is a Graph for number
of beds vs cost of the property: Following things can be observed from the above two graphs:
Observation:

1. The number of properties is inversely proportional to the number of beds.
2. The price of the listed property increases with the number of beds available in the property.

Understanding the host verification in figure 8:

```
Figure 8
```
Observation: The above graph shows that majority of the hosts have between 4 to 7 verifications.


Understanding the impact of a property type on its price in figure 9:

```
Figure 9
```
Observation: The average price is moving on the upside as we go towards spacious property types.

The relation between price and number of people a property can accommodate can be seen in
figure 10:

```
Figure 10
```
Observation: The number of people a property can accommodate and the property type both play an
essential role & are correlated to the property's price.


## Data Analysis.

From the above analysis, we understand that room price and property type play an important role
and are correlates to the price of the property. Thus, to understand the relation, we calculate the
Pearson correlation between the features of the data. However, some of the above features are in the
string format. Before further processing, we need to perform string indexing on these features.

The calculated correlation of features is shown in figure 11 with Features on the x-axis:

```
Figure 11
```
Observation: A clear & significant impact of features such as room type, property type, bedrooms,
longitude, number of beds, and the number of people a property can accommodate on deciding a
favorable fare for the property.

Once the correlation has been calculated, we calculated we filter the columns with a correlation of
less than 0.5. The columns are filtered to reduce the dimensions of the independent variables.

Before feeding the data to the model, One Hot Encoding is performed on the String Indexed
columns. The independent variables have a large portion of binary features; thus, the ensemble
model Random Forest Regressor is used to learn and generalize the data.

After training the model, we plot predictions in figure 12 to better understand our engine's
performance.


```
Figure 12
```
Observation: Both Predicted and actual values are following a similar trend.

The root means square value for assessing our model

The RSME of the model is 54.771, with the average of the dependent variable (price) is 145. Thus
we can now recommend the price of properties that will be newly listed.

## Improvisation.

The Data file is downloaded from google bucket. The dataset in this bucket is updated every 15
days. Script used to update this bucket is shown in figure 13, and the crontab setting to run the script
every 15 days, as shown in figure 14. The reason to update the file is to add new listings to the
dataset and improve the performance to adapt to the latest trends.

```
Figure 13
```

```
Figure 14
```
## Conclusion.

Thus, we have successfully extracted features that can be used for recommending prices for a new
listing. The date of registration does not play a significant role in determining the cost of the
property. However, features such as room type, property type, bedrooms, longitude, number of beds,
and the number of people a property can accommodate can be used to recommend a favorable fare.

Random Forest Regressor is used to predict the ideal price of the property. The model has an RSME
value of 54.771 and is reasonably suitable for the application. The performance of the
recommendation engines can be improved by using complex modeling techniques and tuning
hyperparameters.

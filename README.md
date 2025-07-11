# US Power Outage Analysis
Data Analysis and Predictive Modeling of US Power Outages

Nathan Ko, Walter Wong

Website: https://waltercywong.github.io/US-Power-Outage-Modeling/

# Introduction and Question Identification

Power outages are a large concern to functioning societies, with massive implications for daily life, commerce, and infrastructure. This report focuses on a comprehensive data cleaning and analysis of a major power outage dataset covering the continental U.S. from January 2000 to July 2016. The dataset, provided by the Laboratory for Advancing Sustainable Critical Infrastructure (LASCI), offers a unique opportunity to explore the patterns and potential causes of power outages. We can examine the distribution of outages and their correlation with demographic and geographical variables to come up with a more targeted approach to maintenance and develeopment of infrastructure in the future. Analyzing this data, there can be responsive changes taken in order to minimize the devastating effects of power outages. 

**Question:** Are power outages worse during the summer? 

**Null hypothesis:** The summer months (7, 8, 9) have the same average number of customers affected as the rest of the year.

**Alternate hypothesis:** The summer months have greater power outages than rest of the year.

The cleaned dataframe has 54 features and 1534 observations.

**Relevant columns:**
- `U.S._STATE`: Represents all the states in the continental U.S.
- `YEAR`: Indicates the year when the outage event occurred
- `MONTH`: Indicates the month when the outage event occurred
- `CUSTOMERS.AFFECTED`: Number of customers affected by the power outage event
- `CLIMATE.REGION`: U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.)
- `DEMAND.LOSS.MW`: Amount of peak demand lost during an outage event (in Megawatt) [but in many cases, total demand is reported]
- `TOTAL.PRICE`: Average monthly electricity price in the U.S. state (cents/kilowatt-hour)
- `TOTAL.CUSTOMERS`: Annual number of total customers served in the U.S. state
- `POPULATION`: Population in the U.S. state in a year

# Data Cleaning

In the original data in the excel file, the 5 rows are unwanted as they are just the title and some notes about the data. The dataframe and its columns "start" from the 6th row downward. Additionally, below the columns, there is a row to specify the units of the column if necessary. We also removed this columns when cleaning the data as there are no actual observations.

At this point, the data being loaded has all the columns and observations in the excel file data. However, the columns ``OUTAGE.START.DATE`` and ``OUTAGE.START.TIME`` can be combined as the first always has a time of "00:00:00". The same is true for the restoration date and time. We combined these columns into ``OUTAGE.START`` and ``OUTAGE.RESTORATION``, dropping the original 4.


|   OBS |   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   RES.PRICE |   COM.PRICE |   IND.PRICE |   TOTAL.PRICE |   RES.SALES |   COM.SALES |   IND.SALES |   TOTAL.SALES |   RES.PERCEN |   COM.PERCEN |   IND.PERCEN |   RES.CUSTOMERS |   COM.CUSTOMERS |   IND.CUSTOMERS |   TOTAL.CUSTOMERS |   RES.CUST.PCT |   COM.CUST.PCT |   IND.CUST.PCT |   PC.REALGSP.STATE |   PC.REALGSP.USA |   PC.REALGSP.REL |   PC.REALGSP.CHANGE |   UTIL.REALGSP |   TOTAL.REALGSP |   UTIL.CONTRI |   PI.UTIL.OFUSA |   POPULATION |   POPPCT_URBAN |   POPPCT_UC |   POPDEN_URBAN |   POPDEN_UC |   POPDEN_RURAL |   AREAPCT_URBAN |   AREAPCT_UC |   PCT_LAND |   PCT_WATER_TOT |   PCT_WATER_INLAND | OUTAGE.START        | OUTAGE.RESTORATION   |
|------:|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:-------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|------------:|------------:|------------:|--------------:|------------:|------------:|------------:|--------------:|-------------:|-------------:|-------------:|----------------:|----------------:|----------------:|------------------:|---------------:|---------------:|---------------:|-------------------:|-----------------:|-----------------:|--------------------:|---------------:|----------------:|--------------:|----------------:|-------------:|---------------:|------------:|---------------:|------------:|---------------:|----------------:|-------------:|-----------:|----------------:|-------------------:|:--------------------|:---------------------|
|     1 |   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | normal             | severe weather     | nan                     |               nan |              3060 |              nan |                70000 |       11.6  |        9.18 |        6.81 |          9.28 |     2332915 |     2114774 |     2113291 |       6562520 |      35.5491 |      32.225  |      32.2024 |         2308736 |          276286 |           10673 |           2595696 |        88.9448 |        10.644  |       0.411181 |              51268 |            47586 |          1.07738 |                 1.6 |           4802 |          274182 |       1.75139 |             2.2 |      5348119 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |
|     2 |   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | intentional attack | vandalism               |               nan |                 1 |              nan |                  nan |       12.12 |        9.71 |        6.49 |          9.28 |     1586986 |     1807756 |     1887927 |       5284231 |      30.0325 |      34.2104 |      35.7276 |         2345860 |          284978 |            9898 |           2640737 |        88.8335 |        10.7916 |       0.37482  |              53499 |            49091 |          1.08979 |                 1.9 |           5226 |          291955 |       1.79    |             2.2 |      5457125 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |
|     3 |   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | cold               | severe weather     | heavy wind              |               nan |              3000 |              nan |                70000 |       10.87 |        8.19 |        6.07 |          8.15 |     1467293 |     1801683 |     1951295 |       5222116 |      28.0977 |      34.501  |      37.366  |         2300291 |          276463 |           10150 |           2586905 |        88.9206 |        10.687  |       0.392361 |              50447 |            47287 |          1.06683 |                 2.7 |           4571 |          267895 |       1.70627 |             2.1 |      5310903 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |
|     4 |   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | severe weather     | thunderstorm            |               nan |              2550 |              nan |                68200 |       11.79 |        9.25 |        6.71 |          9.19 |     1851519 |     1941174 |     1993026 |       5787064 |      31.9941 |      33.5433 |      34.4393 |         2317336 |          278466 |           11010 |           2606813 |        88.8954 |        10.6822 |       0.422355 |              51598 |            48156 |          1.07148 |                 0.6 |           5364 |          277627 |       1.93209 |             2.2 |      5380443 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |
|     5 |   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | warm               | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |       13.07 |       10.16 |        7.74 |         10.43 |     2028875 |     2161612 |     1777937 |       5970339 |      33.9826 |      36.2059 |      29.7795 |         2374674 |          289044 |            9812 |           2673531 |        88.8216 |        10.8113 |       0.367005 |              54431 |            49844 |          1.09203 |                 1.7 |           4873 |          292023 |       1.6687  |             2.2 |      5489594 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |

# Univariate Analysis

## Power Outages by Region

<iframe src="assets/plot_univar_1.html" width=800 height=600 frameBorder=0></iframe>

### Explanation of Graph: 'Power Outages by Region'
This is a graph displaying the distributions of power outages within climate regions in the U.S. 

It is evident that the Northeast region has the highest number of power outages, totaling 350, while the West North Central region has the least, with fewer than 20 outages. For the most part, the other regions fall between 100 to 250 outages.

## Power Outages by Month

<iframe src="assets/plot_univar_2.html" width=800 height=600 frameBorder=0></iframe>

# Bivariate Analysis

## State Proportions of Customers

<iframe src="assets/plot_bivar_1.html" width=800 height=600 frameBorder=0></iframe>

### Explanation of Graph: 'State Proportions of Customers'
This graph displays the proportion of customers to the population mean over the years of each state.

There isn't particularly any state that is a significant outlier. Hawaii and Maine have a small customer base while Maine has a surprising amount. 

# Interesting Aggregates

## Mean Price vs Mean Customers per State


| U.S._STATE           |   TOTAL.PRICE |   TOTAL.CUSTOMERS |
|:---------------------|--------------:|------------------:|
| Alabama              |       7.994   |       2.40059e+06 |
| Alaska               |     nan       |  273530           |
| Arizona              |       9.12214 |       2.79737e+06 |
| Arkansas             |       7.6208  |       1.53684e+06 |
| California           |      13.0885  |       1.47257e+07 |
| Colorado             |       9.122   |       2.50052e+06 |
| Connecticut          |      16.1067  |       1.60595e+06 |
| Delaware             |      11.1408  |  453606           |
| District of Columbia |      12.274   |  254703           |
| Florida              |       9.15578 |       9.30554e+06 |
| Georgia              |       8.29176 |       4.49572e+06 |
| Hawaii               |      23.92    |  468228           |
| Idaho                |       6.53429 |  796922           |
| Illinois             |       8.60711 |       5.62959e+06 |
| Indiana              |       7.77116 |       3.10128e+06 |
| Iowa                 |       7.4925  |       1.56198e+06 |
| Kansas               |       8.97875 |       1.46459e+06 |
| Kentucky             |       6.80692 |       2.23165e+06 |
| Louisiana            |       7.948   |       2.24188e+06 |
| Maine                |      12.9742  |  788618           |
| Maryland             |      10.8629  |       2.43764e+06 |
| Massachusetts        |      13.6011  |       3.08185e+06 |
| Michigan             |       9.44915 |       4.79143e+06 |
| Minnesota            |       9.01    |       2.59851e+06 |
| Mississippi          |       9.4525  |       1.5018e+06  |
| Missouri             |       8.13706 |       3.07634e+06 |
| Montana              |       8.37667 |  586390           |
| Nebraska             |       6.9125  |  975464           |
| Nevada               |       8.54714 |       1.25578e+06 |
| New Hampshire        |      14.4786  |  708129           |
| New Jersey           |      14.1009  |       3.95319e+06 |
| New Mexico           |       8.7625  |  991842           |
| New York             |      15.42    |       8.01265e+06 |
| North Carolina       |       8.45135 |       4.76943e+06 |
| North Dakota         |       7.56    |  380216           |
| Ohio                 |       8.58279 |       5.49311e+06 |
| Oklahoma             |       7.49826 |       1.95627e+06 |
| Oregon               |       8.2324  |       1.91001e+06 |
| Pennsylvania         |       9.90054 |       5.94092e+06 |
| South Carolina       |       7.75875 |       2.31443e+06 |
| South Dakota         |       7.67    |  436229           |
| Tennessee            |       9.19636 |       3.21463e+06 |
| Texas                |       9.09185 |       1.10837e+07 |
| Utah                 |       7.73976 |       1.11139e+06 |
| Vermont              |      14.2867  |  361019           |
| Virginia             |       8.22361 |       3.57355e+06 |
| Washington           |       6.92917 |       3.2302e+06  |
| West Virginia        |       7.9425  |       1.01609e+06 |
| Wisconsin            |       9.849   |       2.94078e+06 |
| Wyoming              |       6.815   |  328024           |



### Explanation of DataFrame: 'Mean Price vs Mean Customers per State'
'Mean Price vs Mean Customers per State' reveals how the price and number of customers fluctuate for each state. States that have high prices while having a low number of customers and vice versa, revealing the cost of living for each state. 

# Assessment of Missingness

## NMAR Analysis
Column that we think is NMAR: ``CAUSE.CATEGORY.DETAIL``

``CAUSE.CATEGORY.DETAIL`` is a detailed description of the event categories causing the major power outages. It is NMAR because the cause doesnt fit in one of the limited categories due to being a multitude of causes. To possibly collect more data to make it MAR, we can have someone present at the site of the power outage and provide detailed observations of everything going on there. From this text, we can parse it for observations previously present in CAUSE.CATEGORY.DETAIL and count the number of unique observations we see. If the missing is correlated to higher counts of these occurrences, we can say that ``CAUSE.CATEGORY.DETAIL`` is MAR due to not being able to put a certain outage in a single category.

## MAR Analysis

**MAR Question:** Is ``CUSTOMERS.AFFECTED`` missing dependent on ``CLIMATE.CATEGORY``?

**Null hypothesis:** ``CUSTOMERS.AFFECTED`` is not missing dependent on ``CLIMATE.CATEGORY``.\
**Alternative hypothesis:** ``CUSTOMERS.AFFECTED`` is missing dependent on ``CLIMATE.CATEGORY``.
 
Working with a significance level of 5%, we cannot reject the null hypothesis because the p_value above is signifcantly higher than 0.05. As a result, we cannot make a conclusion on whether the missingness of ``CUSTOMERS.AFFECTED`` is dependent on ``CLIMATE.CATEGORY``.

**MAR Question:** Is ``CUSTOMERS.AFFECTED`` missing dependent on ``U.S._STATE``?

**Null hypothesis:** ``CUSTOMERS.AFFECTED`` is not missing dependent on ``U.S._STATE``.\
**Alternative hypothesis:** ``CUSTOMERS.AFFECTED`` is missing dependent on ``U.S._STATE``.

### Distributions of US States, Missing vs Not for Customers Affected 

<iframe src="assets/plot_mar_1.html" width=800 height=600 frameBorder=0></iframe>

### Empirical Distribution of Test Statistics

<iframe src="assets/plot_mar_2.html" width=800 height=600 frameBorder=0></iframe>

Note: Red hash is the observed test statistic.

### MAR Analysis Conclusion

Working with a significance level of 5% , we can reject the null hypothesis because the p_value above is signifcantly lower than 0.05. As a result, we can conclude that the missingness of ``CUSTOMERS.AFFECTED`` is dependent on ``U.S._STATE``.

# Hypothesis Testing

**Question**: Are power outages worse during the summer compared to the rest of year?

To more specifically explore our question, we define the severity of power outages by how many customers are being affected and the summer consitutes of July, August, and September.

**Null Hypothesis:** The summer months of July, August, and September have the same average number of customers affected as the rest of the year.

**Alternative Hypothesis:** The summer months of July, August, and September have a greater average number of customers affected versus the rest of the year.

**Test Statistic:** The mean of ``CUSTOMERS.AFFECTED`` for the whole year subtracted from the mean of ``CUSTOMERS.AFFECTED`` in the summer months.

This is a good test statistic as a large test statistic means that there is a significance difference between the severity of outages in the summer vs the rest of the year. Under the null, this test statistic should also be zero. Additionally, since we are only finding if power outages are **worse** during the summer, we only need to compare if the simulated test statistics are larger than the observed.

**Significance Level:** 5% 

### Hypothesis Testing Conclusion

Since the p-value above is significantly less than the significance level of 5%, we can reject the null hypothesis and conclude that it is likely power outages are worse during the summer compared to the rest of the year. This makes sense, as customers are more likely to turn on their AC during the hotter summer months, putting a greater strain on the electrical grid.

# Modeling_US_Power_Outages

### Framing the Problem
Power outages are a large concern to functioning societies, with massive implications for daily life, commerce, and infrastructure. However, the underlying cause of power outages can vary from natural disasters to equipment failure. To be cognizant of the power outage's cause can provide insight to appropriately respond to each case. For instance, when a power outage results from a xxx, the impact can be devastating with prolonged after effects. On the other hand, outages caused by human error or technical issues often represent a minor inconvenience. 

By understanding the underlying cause of a power outage, communities can better prepare and respond appropriately, whether it involves implementing robust disaster recovery plans for natural disasters or focusing on regular maintenance and upgrades to mitigate the risk of equipment failures. This awareness enables a more targeted and efficient approach to minimize the impact of power outages on society at large.


We aim to train a classification model using this data that can assist in identifying the CAUSE.CATEGORY of the power outage.

### Data Cleaning
In the original data in the excel file, the 5 rows are unwanted as they are just the title and some notes about the data. The dataframe and its columns "start" from the 6th row downward. Additionally, below the columns, there is a row to specify the units of the column if necessary. We also removed this columns when cleaning the data as there are no actual observations.

At this point, the data being loaded has all the columns and observations in the excel file data. However, the columns OUTAGE.START.DATE and OUTAGE.START.TIME can be combined as the first always has a time of "00:00:00". The same is true for the restoration date and time. We combined these columns into OUTAGE.START and OUTAGE.RESTORATION, dropping the original 4.

### Prediction Problem: Classification
The prediction problem is to classify the causes of power-outages and we will try to predict all of the power-outage in the U.S.. 

### Response Variable
We will be using multiclassification.
The response variable will be the CAUSE.CATEGORY which has these options:
- 'severe weather'
- 'intentional attack'
- 'system operability disruption'
- 'public appeal', 
- 'equipment failure', 
- 'fuel supply emergency'
- 'islanding'"

### Model Information

We will use Random Forest Classifer in order to predict the CAUSE.CATEGORY. We will use accuracy as it is the most suitable metric in predicting the result since the data set are balanced: There’s an equal amount of win and lose, and we will treat both FP (False Positive) and FN (False Negative) as equally important. Thus it is more suitable than the F-1 score, precision, and recall

We will choose features that will be available during the power-outage and not after. The cause of the power-outage is usually the last feature assigned. 

# Baseline Model

#### Model Description
We will try to predict the cause of power-outages based on selected features while feature engineering with one-hot-encoding for the categorical features. 
The features chosen for this model were 'CLIMATE.CATEGORY', 'TOTAL.PRICE' and 'OUTAGE.DURATION'

#### Features
The model uses one-hot-encoding in order to convert the categorical feature 'CAUSE.CATEGORY' into a numerical feature. We held the numerical features as the same.
- 'CLIMATE.CATEGORY': A categorical feature that provides information about the climate.
- 'TOTAL.PRICE': A quantitative feature that indicates the verage monthly electricity price in the U.S. state (cents/kilowatt-hour)
- 'OUTAGE.DURATION': A quantitative feature that indicates the duration of outage events (in minutes)

#### Model Performance 
The model achieved a testing accuracy of 69.62%. Although the relatively low accuracy indicates that our model needs further evaluation and refinement, it shows that we are on the right track. We could improve on the model using more features and feature-engineering by one-hot-encoding categorical features and transforming the numerical features. 

# Final Model
### Model Features

We choses these features to classify our model:
- CLIMATE.CATEGORY: Transformed using one-hot encoding. This feature represents the climate category of the outage and offers insights into the climate region. The climate may indicate the kind of power-outage occured.  

- CUSTOMERS.AFFECTED: Log-transformed due to a large cluster of zeroes and large values. This feature represents categories of all the events causing the major power outages. The number of customers affected may be an indicator of how vast the power-outage stretches. 

- TOTAL.PRICE: This feature represents the average monthly electricity price in the U.S. state (cents/kilowatt-hour). This may be an indicator of how the cost of power-outages can range. 

- OUTAGE.DURATION: This feature represents the duration of the outage in minutes. Scaling helps handle features with different scales and magnitudes. The duration of the outage may be related to the type of power-outage causing varying lengths of power-outages. 

### Model Performance

We achieved a testing accuracy of 82.93%. We utilized GridSearchCV in order to find the best hyperparameters. We chose to find number of estimators, maximum features, and minimum sample splits which improved our accuracy slightly. Including more features and feature-enginnering them resulted in a better performing model than the baseline model with accuracy of 69.62%. 

## Fairness Analysis
Fairness group choice:
Does our model predict worse if the region in the south or elsewhere.

Null Hypothesis:
Our model has the same prediction accuracy being trained on data from the south vs. data elsewhere.


Alternative Hypothesis:
Our model has a worse prediction accuracy being trained on data from the south vs. data elsewhere.


Test Statistic:
Difference in accuracy

Signficant level:
0.01

### Permutation Test
We found the observed difference of accuracy between data from the south and the data elsewhere. Then we shuffled the CLIMATE.REGION column to see if there is a change in accuracy. Then we find the permuted difference of accuracy between data from the data from the south and data elsewhere. After permutation testing, we resulted in a p-value of 0.187. This is higher than our significant level of 0.01. Therefore, we fail to reject the null hypothesis and claim that our model predicts the same being trained on data from the south and data elsewhere.  

## File Structure
```
|
├───data
│   ├───outage.xlsx
│ 
├───assets
│   ├───plot_agg_1.html
│   ├───plot_bivar_1.html
│   ├───plot_mar_1.html
│   ├───plot_mar_2.html
│   ├───plot_univar_1.html
│   ├───plot_univar_2.html
│ 
├───project_notebook.ipynb
├───README.md
└───requirements.txt
```



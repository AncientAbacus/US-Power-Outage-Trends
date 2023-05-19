# US Power Outage Trends Across Seasons and Climates
By Gino Angelici (gangelici@ucsd.edu) and Ifunanya Okoroma (iokoroma@ucsd.edu) <br />
A project for DSC 80: Practice and Application of Data Science taught at UC San Diego during the Spring 2023 quarter

## Introduction

For this project, we decided to look at a dataset that summarized all major power outages in the continental United States. The data ranged from January 2000 to July 2016. The dataset contains 1534 rows (observations) and 56 columns (variables). Upon investigating and cleaning the data, we came up with the question: <br />
<br />

 What characteristics of these power outages are associated with each season and climate category?

 <br />
 By answering this question, we hope to provide better insight into how weather causes power outages and what time of year these types of outages are most prevalent. For our research, we looked at the columns of climate category, outage causes, outage durations, months, state names and state postal codes. The outage causes column contains strings that relate to what caused the observed power outage. Outage duration is tracked in minutes and months are tracked with floats.

## Cleaning
We commenced a very thorough data cleaning process. Our dataset was collecting using a Microsoft Excel (.xlsx) file. Before converting to a .csv file, we manually removed the first five rows and the two columns as these were not actually data entries. They served as basic description of the dataset that were not a part of the table. These manual changes made it much easier to work with the converted .csv file in Jupyter Notebook. <br />

These were our next steps: <br />

1. Taking a row of units and concatenating those to the column names so they would not be recognized as actual data entries. Dropping that row from the dataframe afterwards. <br />
2. Combining the 'OUTAGE.START.DATE' and 'OUTAGE.START.TIME' columns to make them one column ('OUTAGE.START') to represent the time the power went out as a pandas datetime type. Then, dropping the two columns since they are not needed anymore. <br />
3. Combining the 'OUTAGE.RESTORATION.DATE' and 'OUTAGE.RESTORATION.TIME' columns to make them one column ('OUTAGE.RESTORATION') to represent the time the power was restored as a pandas datetime type. Then, dropping the two columns since they are not needed anymore. <br />
4. Manually checking each column to assess the type of the values in that column. We changed them accordingly to have them make more sense (ex: changing the type of the 'YEAR' column to an 'Int64' type instead of 'float'). <br /> 

Cleaned Dataset:

|   OBS |   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION | DEMAND.LOSS.MW   | CUSTOMERS.AFFECTED   |   RES.PRICE |   COM.PRICE |   IND.PRICE |   TOTAL.PRICE |   RES.SALES |   COM.SALES |   IND.SALES |   TOTAL.SALES |   RES.PERCEN |   COM.PERCEN |   IND.PERCEN |   RES.CUSTOMERS |   COM.CUSTOMERS |   IND.CUSTOMERS |   TOTAL.CUSTOMERS |   RES.CUST.PCT |   COM.CUST.PCT |   IND.CUST.PCT |   PC.REALGSP.STATE |   PC.REALGSP.USA |   PC.REALGSP.REL |   PC.REALGSP.CHANGE |   UTIL.REALGSP |   TOTAL.REALGSP |   UTIL.CONTRI |   PI.UTIL.OFUSA |   POPULATION |   POPPCT_URBAN |   POPPCT_UC |   POPDEN_URBAN |   POPDEN_UC |   POPDEN_RURAL |   AREAPCT_URBAN |   AREAPCT_UC |   PCT_LAND |   PCT_WATER_TOT |   PCT_WATER_INLAND | OUTAGE.START        | OUTAGE.RESTORATION   | SEASON   |
|------:|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:-------------------|:-------------------|:------------------------|------------------:|------------------:|:-----------------|:---------------------|------------:|------------:|------------:|--------------:|------------:|------------:|------------:|--------------:|-------------:|-------------:|-------------:|----------------:|----------------:|----------------:|------------------:|---------------:|---------------:|---------------:|-------------------:|-----------------:|-----------------:|--------------------:|---------------:|----------------:|--------------:|----------------:|-------------:|---------------:|------------:|---------------:|------------:|---------------:|----------------:|-------------:|-----------:|----------------:|-------------------:|:--------------------|:---------------------|:---------|
|     1 |   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | normal             | severe weather     | nan                     |               nan |        51         | <NA>             | 70000                |       11.6  |        9.18 |        6.81 |          9.28 | 2.33292e+06 | 2.11477e+06 | 2.11329e+06 |   6.56252e+06 |      35.5491 |      32.225  |      32.2024 |     2.30874e+06 |          276286 |           10673 |       2.5957e+06  |        88.9448 |        10.644  |         0.4112 |              51268 |            47586 |          1.07738 |                 1.6 |           4802 |          274182 |       1.75139 |             2.2 |  5.34812e+06 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  | Summer   |
|     2 |   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | intentional attack | vandalism               |               nan |         0.0166667 | <NA>             | <NA>                 |       12.12 |        9.71 |        6.49 |          9.28 | 1.58699e+06 | 1.80776e+06 | 1.88793e+06 |   5.28423e+06 |      30.0325 |      34.2104 |      35.7276 |     2.34586e+06 |          284978 |            9898 |       2.64074e+06 |        88.8335 |        10.7916 |         0.3748 |              53499 |            49091 |          1.08979 |                 1.9 |           5226 |          291955 |       1.79    |             2.2 |  5.45712e+06 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  | Spring   |
|     3 |   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | cold               | severe weather     | heavy wind              |               nan |        50         | <NA>             | 70000                |       10.87 |        8.19 |        6.07 |          8.15 | 1.46729e+06 | 1.80168e+06 | 1.9513e+06  |   5.22212e+06 |      28.0977 |      34.501  |      37.366  |     2.30029e+06 |          276463 |           10150 |       2.58690e+06 |        88.9206 |        10.687  |         0.3924 |              50447 |            47287 |          1.06683 |                 2.7 |           4571 |          267895 |       1.70627 |             2.1 |  5.3109e+06  |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  | Fall     |
|     4 |   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | severe weather     | thunderstorm            |               nan |        42.5       | <NA>             | 68200                |       11.79 |        9.25 |        6.71 |          9.19 | 1.85152e+06 | 1.94117e+06 | 1.99303e+06 |   5.78706e+06 |      31.9941 |      33.5433 |      34.4393 |     2.31734e+06 |          278466 |           11010 |       2.60681e+06 |        88.8954 |        10.6822 |         0.4224 |              51598 |            48156 |          1.07148 |                 0.6 |           5364 |          277627 |       1.93209 |             2.2 |  5.38044e+06 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  | Summer   |
|     5 |   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | warm               | severe weather     | nan                     |               nan |        29         | 250              | 250000               |       13.07 |       10.16 |        7.74 |         10.43 | 2.02888e+06 | 2.16161e+06 | 1.77794e+06 |   5.97034e+06 |      33.9826 |      36.2059 |      29.7795 |     2.37467e+06 |          289044 |            9812 |       2.67353e+06 |        88.8216 |        10.8113 |         0.367  |              54431 |            49844 |          1.09203 |                 1.7 |           4873 |          292023 |       1.6687  |             2.2 |  5.48959e+06 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  | Summer   |

Cleaned Dataset with Relevant Columns:

|   OBS |   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | CAUSE.CATEGORY     |   OUTAGE.DURATION | SEASON   |
|------:|-------:|--------:|:-------------|:--------------|----------------:|:-------------------|:-------------------|------------------:|:---------|
|     1 |   2011 |       7 | Minnesota    | MN            |            -0.3 | normal             | severe weather     |        51         | Summer   |
|     2 |   2014 |       5 | Minnesota    | MN            |            -0.1 | normal             | intentional attack |         0.0166667 | Spring   |
|     3 |   2010 |      10 | Minnesota    | MN            |            -1.5 | cold               | severe weather     |        50         | Fall     |
|     4 |   2012 |       6 | Minnesota    | MN            |            -0.1 | normal             | severe weather     |        42.5       | Summer   |
|     5 |   2015 |       7 | Minnesota    | MN            |             1.2 | warm               | severe weather     |        29         | Summer   |

## Exploratory Data Analysis (EDA)
We explored this dataset with various univariate and bivariate analyses and utilized different ways to display them. <br />

We first explored the frequency of the causes of the power outages and saw that most of them came from severe weather events. <br />

<iframe src="assets/UP1.html" width=800 height=600 frameBorder=0></iframe>
 
Here, we created a histogram to understand the amount of power outages that went on for a certain amount of time. Most of the power outages had a small 'OUTAGE.DURATION', meaning they were resolved within a few hours. Meanwhile, there were far fewer that took many hours to get the power restored. <br />

<iframe src="assets/UP2.html" width=800 height=600 frameBorder=0></iframe>
 
 The following four visualizations map the different concentrations of power outages in the United States throughout the four different seasons. <br />

<iframe src="assets/UP3_Spring.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/UP4_Summer.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/UP5_Fall.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/UP6_Winter.html" width=800 height=600 frameBorder=0></iframe>
 
The following is a bar chart, which displays a bivariate analysis of the average 'OUTAGE.DURATION' throughout each season of the year. Throughout the fall and winter seasons of the year in the U.S., power tends to be out for longer.

<iframe src="assets/BP1.html" width=800 height=600 frameBorder=0></iframe>
 
The second bivariate analysis is another bar chart, which displays a bivariate analysis of the average 'OUTAGE.DURATION' throughout each 'CLIMATE.CATEGORY' a power outage was classified under. With the warmer climates, power tends to be out for longer.

<iframe src="assets/BP2.html" width=800 height=600 frameBorder=0></iframe>

### Pivot Table: Used to observed the concentration of power outages throughout the four seasons of the year <br />
Note: Further data cleaning was necessary to display this pivot table in the desired format. The 'MONTH' data was initially represented as integers. The type of the column needed to be converted to strings before they were replaced with the appropriate season that corresponded to that month.

| SEASON   | CAUSE.CATEGORY   |   OBS |   OUTAGE.DURATION |
|:---------|:-----------------|------:|------------------:|
| Fall     | severe weather   |   158 |           94.1019 |
| Spring   | severe weather   |   125 |           54.7947 |
| Summer   | severe weather   |   283 |           53.0054 |
| Winter   | severe weather   |   193 |           64.4887 |

## Assessment of Missingness
While conducting our EDA, we noticed that the 'OUTAGE.START' had missing values that would also affect the missingness of other columns such as 'OUTAGE.RESTORATION' and 'OUTAGE.DURATION', along with the construction of 'SEASON' as and added a column along with being used in our pivot table. We investigated further to understand why this was. Here, we formulated our missingness assessments in the form of hypothesis tests. <br />

When assessing missingness, we asked two questions that focused primarly on the 'OUTAGE.DURATION' column and its missingness dependence. <br />

### 1. Is the missingness of 'OUTAGE.DURATION' dependent on the values of 'CLIMATE.CATEGORY'? <br />
Null: The distribution of 'CLIMATE.CATEGORY' when 'OUTAGE.DURATION' is missing is the same as the distribution of 'CLIMATE.CATEGORY' when 'OUTAGE.DURATION' is not missing. <br />
Alternative: The distribution of 'CLIMATE.CATEGORY' when 'OUTAGE.DURATION' is missing is different than the distribution of 'CLIMATE.CATEGORY' when 'OUTAGE.DURATION' is not missing. <br />
Significance Level: 0.05 <br />
 
To check this, we looked at the missingness of 'OUTAGE.DURATION' conditioned on 'CLIMATE.CATEGORY'. The implementation for this was to complete a permutation test and use the total variation distance (TVD) as our test statistic. With a p-value less than our cutoff at 0.05, we can determine that the missingness of 'OUTAGE.DURATION' is dependent on 'CLIMATE.CATEGORY'. In this case, the 'OUTAGE.DURATION' column is Missing at Random (MAR). <br />

<iframe src="assets/EM1.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/TM1.html" width=800 height=600 frameBorder=0></iframe>

### 2. Is the missingness of 'OUTAGE.DURATION' dependent on the values of 'SEASON'? <br />
Null: The distribution of 'SEASON' when 'OUTAGE.DURATION' is missing is the same as the distribution of 'SEASON' when 'OUTAGE.DURATION' is not missing. <br />
Alternative: The distribution of 'SEASON' when 'OUTAGE.DURATION' is missing is different than the distribution of 'SEASON' when 'OUTAGE.DURATION' is not missing. <br />
Significance Level: 0.05 <br />

To check this, we looked at the missingness of 'OUTAGE.DURATION' conditioned on 'SEASON'. The implementation for this was to complete a permutation test and use the total variation distance (TVD) as our test statistic. With a p-value greater than our cutoff at 0.05, we can determine that the missingness of 'OUTAGE.DURATION' is not dependent on 'SEASON'. In this case, the 'OUTAGE.DURATION' column is Missing Completely at Random (MCAR). <br />

<iframe src="assets/EM2.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/TM2.html" width=800 height=600 frameBorder=0></iframe>

## Hypothesis Testing
For the portion where we had to conduct hypothesis testing, we completed two tests, a hypothesis test and a permutation test. <br />

### Hypothesis Test 1 <br />
Null: The US experiences the same frequency of warm climate severe weather power outages as any other climate category (normal or cold). <br />
Alternative: The US experiences the different frequency of warm climate severe weather power outages than other climate categorues (normal or cold). <br />
Significance Level: 0.05 <br />

To run this hypothesis test, we ran np.random.multinomial, which provides a simulation of tests under the null hypothesis. To calculate the p-value, we found the simulated porportion of warm climates and counted the porportion of those that were above 33%. This communicates how common it is to see warmer climates as greater than 33% of all the climates of the power outage entries. With a p-value cutoff of 0.05, the reject the null hypothesis.

<iframe src="assets/HT2.html" width=800 height=600 frameBorder=0></iframe>

### Hypothesis Test 2 <br />
Null: California experiences the same frequency of severe weather power outages each season as the rest of the country. <br />
Alternative: California experiences a different frequency of severe weather power outages each season as the rest of the country. <br />
Significance Level: 0.05 <br />

We first idenitfied the drastic differences in severe weather power outage distributions between the U.S. and California across all seasons. Noting these differences, we ran a hypothesis test to see if these differences were significant.


|        |   US Severe Weather Outage Distribution |
|:-------|----------------------------------------:|
| Summer |                                0.372859 |
| Winter |                                0.254282 |
| Fall   |                                0.208169 |
| Spring |                                0.16469  |

|        |   CA Severe Weather Outage Distribution |
|:-------|----------------------------------------:|
| Winter |                                0.371429 |
| Fall   |                                0.257143 |
| Summer |                                0.214286 |
| Spring |                                0.157143 |

To run this hypothesis test, we ran np.random.multinomial, which provides a simulation of tests under the null hypothesis. To calculate the p-value, we compared the results of these California distribution simulations with the given population distribution of the U.S. With a p-value cutoff of 0.05, we reject the null hypothesis and conclude that there is evidence to support the claim that California experiences a different frequency of severe weather power outages each season than the rest of the country.

<iframe src="assets/HT1.html" width=800 height=600 frameBorder=0></iframe>

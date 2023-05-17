# US-Power-Outage-Trends
by Gino Angelici (gangelici@ucsd.edu) and Ifunanya Okoroma (iokoroma@ucsd.edu) <br />
a project for DSC 80: Practice and Application of Data Science taught at UC San Diego during the Spring 2023 quarter

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
4. Manually checking each column to assess the type of the values in that column. We changed them accordingly to have them make more sense (ex. changing the type of the 'YEAR' column to an 'Int64' type instead of 'float'). <br /> 

## Exploratory Data Analysis (EDA)
We explored this dataset with various univariate and bivariate analyses and utilized different ways to display them. <br />

### Pivot Table: Used to observed the concentration of power outages throughout the four seasons of the year <br />
Note: Further data cleaning was necessary to display this pivot table in the desired format. The 'MONTH' data was initially represented as integers. The type of the column needed to be converted to strings before they were replaced with the appropriate season that corresponded to that month.

## Assessment of Missingness
While conducting our EDA, we noticed that the 'OUTAGE.START' had missing values that would also affect the missingness of other columns such as 'OUTAGE.RESTORATION', along with the construction of our pivot table. We investigated further to understand why this was.


## Hypothesis Testing
For the portion where we had to conduct hypothesis testing, we completed two tests, a hypothesis test and a permutation test. <br />

### Hypothesis Test <br />
Null: The frequency of a particular climate category is not an indicator of when an outage occurs <br />
Alternative: Warmer climate categories are a better breeding ground to have power outages <br />

### Permutation Test <br />
Null: The state of California experiences the same frequency of power outages as the rest of the country <br />
Alternative: California power outages and power outages for the rest of the country come from two different distributions <br />

# US-Power-Outage-Trends
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

## Exploratory Data Analysis (EDA)
We explored this dataset with various univariate and bivariate analyses and utilized different ways to display them. <br />

<iframe src="assets/UP1.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/UP2.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/UP3_Spring.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/UP4_Summer.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/UP5_Fall.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/UP6_Winter.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/BP1.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/BP2.html" width=800 height=600 frameBorder=0></iframe>

### Pivot Table: Used to observed the concentration of power outages throughout the four seasons of the year <br />
Note: Further data cleaning was necessary to display this pivot table in the desired format. The 'MONTH' data was initially represented as integers. The type of the column needed to be converted to strings before they were replaced with the appropriate season that corresponded to that month.

## Assessment of Missingness
While conducting our EDA, we noticed that the 'OUTAGE.START' had missing values that would also affect the missingness of other columns such as 'OUTAGE.RESTORATION' and 'OUTAGE.DURATION', along with the construction of 'SEASON' as and added a column along with being used in our pivot table. We investigated further to understand why this was. <br />

When assessing missingness, we asked two questions that focused primarly on the 'OUTAGE.DURATION' column and its missingness dependence. <br />

### 1. Is the missingness of 'OUTAGE.DURATION' dependent on the values of 'CLIMATE.CATEGORY'? <br />
To check this, we looked at the missingness of 'OUTAGE.DURATION' conditioned on 'CLIMATE.CATEGORY'. The implementation for this was to complete a permutation test and use the total variation distance (TVD) as our test statistic. With a p-value less than our cutoff at 0.05, we can determine that the missingness of 'OUTAGE.DURATION' is dependent on 'CLIMATE.CATEGORY'.

<iframe src="assets/EM1.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/TM1.html" width=800 height=600 frameBorder=0></iframe>

### 2. Is the missingness of 'OUTAGE.DURATION' dependent on the values of 'SEASON'? <br />
To check this, we looked at the missingness of 'OUTAGE.DURATION' conditioned on 'SEASON'. The implementation for this was to complete a permutation test and use the total variation distance (TVD) as our test statistic. With a p-value greater than our cutoff at 0.05, we can determine that the missingness of 'OUTAGE.DURATION' is not dependent on 'SEASON'.

<iframe src="assets/EM2.html" width=800 height=600 frameBorder=0></iframe>

<iframe src="assets/TM2.html" width=800 height=600 frameBorder=0></iframe>

## Hypothesis Testing
For the portion where we had to conduct hypothesis testing, we completed two tests, a hypothesis test and a permutation test. <br />

### Hypothesis Test <br />
Null: The frequency of a particular climate category is not an indicator of when an outage occurs <br />
Alternative: Warmer climate categories are a better breeding ground to have power outages <br />

To run this hypothesis test, we ran np.random.multinomial, which provides a simulation of tests under the null hypothesis. To calculate the p-value, we found the simulated porportion of warm climates and counted the porportion of those that were above 33%. This communicates how common it is to see warmer climates as greater than 33% of all the climates of the power outage entries.

<iframe src="assets/HT2.html" width=800 height=600 frameBorder=0></iframe>

### Hypothesis Test <br />
Null: The state of California experiences the same frequency of power outages as the rest of the country <br />
Alternative: California power outages and power outages for the rest of the country come from two different distributions <br />

<iframe src="assets/HT1.html" width=800 height=600 frameBorder=0></iframe>

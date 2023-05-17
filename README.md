# US-Power-Outage-Trends
by Gino Angelici (gangelici@ucsd.edu) and Ifunanya Okoroma (iokoroma@ucsd.edu) <br />
a project for DSC 80: Practice and Application of Data Science taught at UC San Diego during the Spring 2023 quarter

## Introduction

For this project, we decided to look at a dataset that summarized all major power outages in the continental United States. The data ranged from January 2000 to July 2016. The dataset contains 1534 rows (observations) and 56 columns (variables). Upon investigating and cleaning the data, we came up with the question: <br />
<br />

 What characteristics of these power outages are associated with each season?

 <br />
 By answering this question, we hope to provide better insight into how weather causes power outages and what time of year these types of outages are most prevalent. For our research, we looked at the columns of climate category, outage causes, outage durations, months, state names and state postal codes. The outage causes column contains strings that relate to what caused the observed power outage. Outage duration is tracked in minutes and months are tracked with floats.

## Cleaning and Exploratory Data Analysis
Once we downloaded the file, we got manually got rid of the first 5 rows and first 2 columns as these contained a basic description of the dataset that was not part of the table. Next, we decided to drop the units row and move the data from this row into a separate dictionary. This allowed us to check the units of each column without changing the names of the columns. The next big step was to combine the start dates and start times of outages in one column called "OUTAGE.START". We did this by 


## Assessment of Missingness


## Hypothesis Testing
For the portion where we had to conduct hypothesis testing, we completed two tests, a hypothesis test and a permutation test. <br />

### Hypothesis Test <br />
Null: The frequency of a particular climate category is not an indicator of when an outage occurs <br />
Alternative: Warmer climate categories are a better breeding ground to have power outages <br />

### Permutation Test <br />
Null: The state of California experiences the same frequency of power outages as the rest of the country <br />
Alternative: California power outages and power outages for the rest of the country come from two different distributions <br />

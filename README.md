# Web Scraping from Indeed.com and Predicting Salaries

![indeed-logo-vector](https://user-images.githubusercontent.com/76961031/117969713-af386980-b31f-11eb-860f-6b65711181d2.png)

The aim of this project was to scrape data from indeed.com and predict whether an observation would be a high or low salary based off job location, key words in the job title (such as 'Machine Learing') and the seniority of the role.

## Table of Contents
- [Introduction](#introduction)
- [Data Collection & Pre-Processing](#data-collection---pre-processing)
- [Modelling](#modelling)
- [Conclusions](#conclusions)
- [Future Work](#future-work)



## Introduction

**Point of View:** You're working as a data scientist for a contracting firm that's rapidly expanding. The firm need to leverage data to win more contracts. Your firm offers technology and scientific solutions and wants to be competitive in the hiring market. Your manager wants you to determine the industry factors that are most important in predicting the salary amounts for data scientists/research scietists.

Aggregators like Indeed.com regularly pool job postings from a variety of markets and industries.

## Data Collection & Pre-Processing

The data was collected using the requests and beautiful soup packages within a singular function that would iteritively add to a list of lists. 
The main preprocessing steps were to dummify the locations and to change the rates of pay to the yearly rate. 

## Modelling

Firstly, models were ran to predict high salary (above the 75% quantile) using only location as the predictor variable. Due to high class imbalance, I used SMOTE to create a y target with a baseline accuracy of 50%. SMOTE generates new observations using euclidean distance to create data points similar to that of the target variable.

Below is a summary table of the models ran without SMOTE and with SMOTE.

![locations_only_no_smote](https://user-images.githubusercontent.com/76961031/117980928-5d4a1080-b32c-11eb-9fe5-7268a4081748.png)
![location_only_smote](https://user-images.githubusercontent.com/76961031/117980956-65a24b80-b32c-11eb-996e-d33b03c43869.png)


## Future Work

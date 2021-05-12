# Web Scraping from Indeed.com and Predicting Salaries

![indeed-logo-vector](https://user-images.githubusercontent.com/76961031/117969713-af386980-b31f-11eb-860f-6b65711181d2.png)

The aim of this project was to scrape data from indeed.com and predict whether an observation would be a high or low salary based off job location, key words in the job title (such as 'Machine Learing') and the seniority of the role.

## Table of Contents
- [Introduction](#introduction)
- [Data Collection & Pre-Processing](#data-collection---pre-processing)
- [Modelling](#modelling)
- [Conclusion](#conclusion)



## Introduction

**Point of View:** You're working as a data scientist for a contracting firm that's rapidly expanding. The firm need to leverage data to win more contracts. Your firm offers technology and scientific solutions and wants to be competitive in the hiring market. Your manager wants you to determine the industry factors that are most important in predicting the salary amounts for data scientists/research scietists.

Aggregators like Indeed.com regularly pool job postings from a variety of markets and industries.

## Data Collection & Pre-Processing

The data was collected using the requests and beautiful soup packages within a singular function that would iteritively add to a list of lists. 
The main preprocessing steps were to dummify the locations and to change the rates of pay to the yearly rate.

Below is how the data frame shaped up after cleaning.

![data_table](https://user-images.githubusercontent.com/76961031/117983271-b155f480-b32e-11eb-86c7-6a428a12cbe4.png)


## Modelling

Firstly, models were ran to predict high salary (above the 75% quantile) using only location as the predictor variable. Due to high class imbalance, I used SMOTEN, an oversampling technique used for when the data is predominently categorical, to create a y target with a baseline accuracy of 50%. SMOTE generates new observations using euclidean distance to create data points similar to that of the target variable.

Below is a summary table of the models ran without SMOTE (baseline of 75%) and with SMOTE.

![locations_only_no_smote](https://user-images.githubusercontent.com/76961031/117980928-5d4a1080-b32c-11eb-9fe5-7268a4081748.png)
![location_only_smote](https://user-images.githubusercontent.com/76961031/117980956-65a24b80-b32c-11eb-996e-d33b03c43869.png)

Secondly, models were ran incorperating the job title variable without SMOTEN and with SMOTEN.

![no_smote](https://user-images.githubusercontent.com/76961031/117981907-62f42600-b32d-11eb-9030-4974fa314175.png)
![smote](https://user-images.githubusercontent.com/76961031/117981930-6687ad00-b32d-11eb-9391-dad59f3179dd.png)


Below are the feature importances/coefficients for the greatest individual models used (logistic regression, support vector machine and decision tree). The support vector machine was used here becuase the knn algorithm doesnt have a coefficient or feature importance feature.

![feature_importance_coefficients](https://user-images.githubusercontent.com/76961031/117983521-f417cc80-b32e-11eb-9f9e-7a07e1af7c37.png)


The best performing model from the SMOTEN dataset was originally a hard voting classifier containing a logistic regression, k nearest nighbors and decision tree classifier.

Finally, a soft voting classifier was used (on SMOTEN data)and yeilded the best results, which are summarised in the images below.

**Confusion Matrix**
![confusion_matrix_soft_vote](https://user-images.githubusercontent.com/76961031/117983305-badf5c80-b32e-11eb-8e67-8dcc80540b3d.png)


**Classification Report**
![classification_report_vote_soft](https://user-images.githubusercontent.com/76961031/117989125-f7618700-b333-11eb-88dc-88a8c33024b9.png)

**Receiver Operating Characteristic Curve (ROC)**
![roc_soft](https://user-images.githubusercontent.com/76961031/117989596-5d4e0e80-b334-11eb-81d6-62c44ea9b6ac.png)

**Precision Recall Curve**
![precision_recall](https://user-images.githubusercontent.com/76961031/117989706-75be2900-b334-11eb-9e48-3e7c8cfeb7e1.png)


## Conclusion
Although the voting classification model successfully reduces the number of fasle positives, it can still be improved significantly. The next steps to improve out model of predicting salary would be to scrape from many more websites such as Glassdoor, Linkedin and Otta. Increasing our salary reach can enlarge our dataset considerably such that we are able represent the population more closely, it also eliminates any bias in our data that may eminate from using one website source. Moreover, much of the data from job postings is locked in the words used to describe them. In a future model I shall consider utilising natural language processing (NLP) to see which words are used more frequently to predict higher salary.




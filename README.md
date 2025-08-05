# LOAN DEFAULT PREDICTION

## INTRODUCTION

The aim of the project is to help banks in Nigeria predict whether new loans to existing borrowers are likely to be repaid or default. 

The project is based on a machine learning competition found on the Zindi website [Zindi](https://zindi.africa/competitions/data-science-nigeria-challenge-1-loan-default-prediction). It uses a dataset relating to loans made by Nigerian banks.    

## DATA

Three data files are provided (these can be downloaded from the Zindi website). Each has a customer id as a common field.

The first is a file of demographic information with one row for each customer (for example age, location, name of bank). 

The second is a file of historic loans, with some customers having multiple loans. This file includes loan amount, length of the loan, repayment due date and repayment actual date and several other fields. 

The third file is a list of proposed new loans with a column indicating whether the loan was repaid or not. The aim is to create a model that can accurately predict whether the new loan will be repaid or not. 

**DATA ENGINEERING**

The historic loan data was flattened (so that there was one line per customer) and then the three files were aggregated into a single file. Some rows were then deleted as they did not have a proposed new loan. Some columns were also deleted as they had a high number of missing data points. After this 'data engineering' the resulting single data file had 3272 rows (customers) and 52 columns (variables). 

The data was split in two a training set (used to train the ML learning model) and test set (used to see if the model is accurate). The split was random with 60% in the training set and 40% in the test set. 

## MODEL

The code initially uses six different machine learning models in order to try to find which one works best. There were three models that produced better results than the others. These three had similar results - RandomForest, AdaBoost and GradientBoost. The results of AdaBoost were marginally better than the others.  All three of the best performing models were ensemble techniques (meaning they create multiple models then combine the results, almost like having lots of different models 'voting' for repaid or defaulted).

After a first run of these models, the data engineering was revisited (deleting some variables variables and balancing the training data, so that the number of examples with default and repaid was equal. Then the models were run a second time. There was an improvement in the performance for the default class but overall there was little change as a result of this second pahse of feature engineering.  

## HYPERPARAMETER OPTIMSATION

Hyper-paramters are variables that can be varied in setting up each model. For each of the models a range of hyper-parameters were tested to try and find the optimum selection, using a technique called grid search.   

## RESULTS AND CONCLUSION

The best performing model was AdaBoost. The results are shown in the table below. The Zindi competition uses accuracy as the measure of success and this model had an accuracy score of 79%. What this means is that 79% of the loans were correctly predicted. However the level of success was much higher for the loans that did not default than for the loans that defaulted. 

In a business siutation, banks need to be able to predict likelihood of default with a high degree of accuracy. This model is not yet accurate enough for business application on its own. Perhaps it could be used alongside human judgement, as an aid to lending decisions. 

Human decision making may also address any potential ethical considerations. Many banking regulators require lending decisions to include a 'human in the loop' so that loans are not granted purely on the basis of a ML model. 

![Screenshot](C:\Users\Simon\OneDrive\Documents\adaBoost_Screenshot%202025-08-03%20181452.png)

## FURTHER WORK

This model was completed in a week and could be further modified to improve accuracy with more time. For example the latitude/longitude information was not fully exploited. One could map these locations onto an urban/rural map, creating a new variable of urban/rural. 

The model may also be improved if some of the missing data was completed or if more data was obtained.   

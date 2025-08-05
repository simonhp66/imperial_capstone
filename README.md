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

The historic loan data was flattened (so that there was one line per customer) and then the three files were aggregated into a single train set. Some rows were then deleted as they did not have a proposed new loan. Some columns were also deleted as they had a high number of missing data points. After this engineering the resulting single data file had 3272 rows (customers) and 52 columns (variables). 

The data was split into a train and test set, with 60% train and 40% test. 

The data was unbalanced with 1536 positive cases (loan repaid) and 427 negative cases (loan defaulted) in the train set. This often leads to inaccurate machine learning models. A process known as 'smote' was used to rebalance the number of cases in the training data.  

## MODEL

The code initially uses six different models in order to try to find which one works best. 

There were three models that produced better results than the others. These three had similar results - RandomForest, AdaBoost and GradientBoost. The results of AdaBoost were marginally better than the others.  All three of the best performing models were ensemble techniques (meaning they create multiple models then combine the results, almost like having lots of different models 'voting' for repaid or defaulted).

After a first run of these models, the data engineering was revisited (deleting variables which had little impact on the final result and also deleting variables which had high correlation with each other. In addition the smote balancing of the training data was performed at this point. 

Then the models were run a second time. There was an improvement in the performance for the minority class but overall there was little change as a result of this feature engineering and smote relablancing. 

## HYPERPARAMETER OPTIMSATION

For each of the 6 models a range of hyper-parameters were tested. Grid search was technique used (GridSearchCV).  The range of each hyper-parameter considered was limited due to the time it takes to run the models. 

For the best performing model (AdaBoost) the hyper-parameters considered were n_estimators and the learning rate. Initially only two posibilities were considered for each of these hyper-parameters. Then in a second run of the models the range was widened, but it had no impact on the end result.  

## RESULTS AND CONCLUSION

The best performing model was AdaBoost. The results are shown in the table below. The Zindi competition uses accuracy as the measure of success and this model had an accuracy score of 79%. Wgat this means is that 79% of the loans were correctly predicted. However the level of success was much higher for the loans that did not default than for the loans that defaulted. 

In a business siutation, banks need to be able to predict likelihood of default with a high degree of accuracy. This model is not yet accurate enough for business application on its own. Perhaps it could be used alongside human judgement, as an aid to lending decisions. 

Human decision making may also address any potential ethical considerations. Many banking regulators require lending decisions to include a 'human in the loop' so that loans are not granted purely on the basis of a ML model. 

![Screenshot](C:\Users\Simon\OneDrive\Documents\adaBoost_Screenshot%202025-08-03%20181452.png)

## FURTHER WORK

This model was completed in a week and could be further modified to improve accuracy with more time. For example the latitude/longitude information was not fully exploited. One could map these locations onto an urban/rural map, creating a new variable of urban/rural. 

The model may also be improved if some of the missing data was completed or if more data was obtained.   

# LOAN DEFAULT PREDICTION

## INTRODUCTION

The project is based on a machine learning competion found on the Zindi website [Zindi](https://zindi.africa/competitions/data-science-nigeria-challenge-1-loan-default-prediction). It uses a datset relating to loans made by Nigerian banks. The aim is to predict whether a selection of new loans will be repaid or default. 

The competition involves submitting answers for a test set and waiting for the score. To circumvent this process, for the purposes of this project, I divided the train set into a train and a test set.   

## DATA

Three data files are provided (these can be downloaded from the Zindi website). Each has a customer id as a common field.

The first is a file of demographic information with one row for each customer (for example age, location, name of bank). 

The second is a file of historic loans, with some customers having multiple loans. This file includes loan amount, length of the loan, repayment due date and repayment actual date. 

The third file is a list of proposed new loans with a column indicating whether the loan was repaid or not. So this column represents the 'Y' value. This is what we are trying to predict.

**DATA ENGINEERING**

The historic loan data was flattened (so that there was one line per customer) and then the three files were aggregated into a single train set. Some rows were then deleted as they did not have a proposed new loan. Some columns were also deleted as they had a high number of missing data points. After this engineering the resulting single data file had 3272 rows (customers) and 52 columns (variables). 

The data was split into a train and test set, with 60% train and 40% test. 

The data in the was unbalanced with 1536 positive cases (loan repaid) and 427 negative cases (loan defaulted) in the train set. This was addressed in the code using smote to balance the data for the train set. 

## MODEL

The code initially uses six different models in order to try to find which one works best. 

There were three models that produced better results than the others. These three had similar results - RandomForest, AdaBoost and GradientBoost. The results of AdaBoost were marginally better than the others.  All three of the best performing models were ensemble techniques (creating multiple models then combining the results).

After a first run of these models, the data engineering was revisited (deleting variables which had little impact on the final result and also deleting variables which had high multi-collinearity). In addition the smote balancing of the train data was performed at this point. 

Then the models were run a second time. There was an improvement in the performance for the minority class but overall there was little change as a result of this feature engineering and smote relablancing. 

  

## HYPERPARAMETER OPTIMSATION

For each of the 6 models a range of hyper-parameters were tested. Grid search was technique used (GridSearchCV).  The range of each hyper-parameter considered was limited due to the time it takes to run the models. 

For the best performing model (AdaBoost) the hyper-parameters considered were n_estimators and the learning rate. Initially only two posibilities were considered for each of these hyper-parameters. Then in a second run of the models the range was widened, but it had no impact on the end result.  

## RESULTS AND CONCLUSION

The best performing model was AdaBoost. The results are shown in the table below. The Zindi competition uses accuracy as the measure of success and this model had an accuracy score of 79%.

However overall I would say that this model is not really accurate enough for business application. In particular the results for the minority class remain poor despite the use of smote to balance the data. Perhaps it could be used alongside human judgement, as an aid to lending decisions. 

Human decision making may also address any potential ethical considerations. Many banking regulators require lending decisions to include a 'human in the loop' so that loans are not granted purely on the basis of a ML model. 

![Screenshot](C:\Users\Simon\OneDrive\Documents\adaBoost_Screenshot%202025-08-03%20181452.png)

## FURTHER WORK

This model was completed in a week and could be further modified to improve accuracy with more time. For example the latitude/longitude information was not fully exploited. One could map these locations onto an urban/rural map, creating a new variable of urban/rural. 

The model may also be improved if some of the missing data was completed or if more data was obtained.   

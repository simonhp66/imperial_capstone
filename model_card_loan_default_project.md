# Model Card



## Model Description

**Input:** Three CSV files (train_demographics; train_prevloans; train_perfloans). These files can be downloaded from the Zindi website. [Zindi website](https://zindi.africa/competitions/data-science-nigeria-challenge-1-loan-default-prediction/data)

*train_demographics.csv *  This file contains demographic information on 4346 bank loan customers

*train_prevloans.csv   *This file contains information relating to 18183 previous loans taken out by these customers including the amount, term and repayment record. 

*train_perfloans.csv*   This file contains information concerning 4638 new loans taken out by the customers including a column indicating whether the loans were repaid or defaulted. 

All three files have a common customer id field for merging them together. 

**Output:** The model produces a binary forecast of whether the new loans will be repaid or not based on demgraphics and previous loan history. 

**Model Architecture:** Initially some Exploratory Data Analysis is conducted. After flattening the train_prevloans.csv file the three files a merged togther. There is some data engineering and cleaning up empty fields. 

The merged train data is then split into a train set (60%) and a test set (40%). 

Six different models are used in order to identify the best performing model. For each model there is some hyper-parameter testing using GridSearchCV. The models are then run using the best hyper-parameters and are assessed based on accuracy. 

List of models: LogisiticRegression, LassoLogistic, RandomForest, GradientBoosting, AdaBoost, KNeighbours, XGBoost and LightGBM

There is then a second phase of data engineering where irrelevant and correlated variables are eliminated from the data set. The datset is unbalanced, and the models perform poorly on the minority class, so the train dataset is then balanced using smote.

The six models are run for a second time, with more extensive hyper-parameter testing for the best performing model.  

## Performance

Three of the models performed and better than the others (AdaBoost, RandomForest, GradientBoosting and XGBoost) with AdaBoost performing marginally better. The performance statistics of AdaBoost are shown below. 

![Photo](C:\Users\Simon\OneDrive\Documents\adaBoost_Screenshot%202025-08-03%20181452.png)

The primary measure of performance is accuracy. At 79% the model is somewhat successful but probably needs either more work or better data in order to be put into production. Despite balancing the data, the model continues to perform poorly for the minority class (representing default). 

 

## Limitations, ethics and bias

The model could be used as an aid to a human making decisions on granting loans but should not be used as a standalone method as it's performance is not yet strong enough. 

The model has been developed based on histroic loan data to this customer group. It should not be used where there is no historic loan data or with customers who have very different attributes from those included in the data set. 

From an ehtical perspective, some banking regulators consider that decisions on whether to grant loans should not be made solely by a machine learning model, that customers have the right to have a human deciding on whether to grant them a loan. In this case the ML model is somewhat opaque (AdaBoost is difficult to explain to non-experts).  

Little information is provided on how the dataset was collected. I am not aware of any bias in the collection of the data. 

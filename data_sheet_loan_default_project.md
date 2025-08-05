# Datasheet Template

## Motivation

- The dataset was created as part of a machine learning competition on the Zindi website 
- It is not clear who created the dataset

## Composition

- The instances in the dataset are people (borrowers from banks) and individual loans (with the borrower as one of the variables). Each person can have multiple historic loans.  
- There are 4346 people, with 18183 historic loans and 4368 new loans.
- There are several fields with over 80% missing data. These field were deleted before processing the data. 
- The data is financial data relating to individual's loans which would be considered confidential, but the individuals cannot easily be identified as the are represented by a customer id rather than a name. 
  
  

## Collection process

- This is not described on the Zindi website.
- It is not clear if this is a sample of a larger dataset.
- The loan information has a date. The earliest date is January 2016 and the latest date is July 2017.

## Preprocessing/cleaning/labelling

- The data was pre-processed in two stages as follows:
- The historic loan data file was 'flattened' so there is a single line for each borrower.
- Some new variables were created such as age (which was bucketed), repayment performance for previous loans (paid early/late) and some aggregate information for previous loans (amounts, terms etc)
- Some variables with more than 80% missing data were deleted from the dataset
- After an intial run of the models, the data was further processed to remove irrelevant variables, to eliminate correlated variables.
- The train data was balanced using smote. 
- Then the models were run again on the balanced data. 
- The original raw data is preserved on the Zindi website and can be downloaded from there. [Zindi](https://zindi.africa/competitions/data-science-nigeria-challenge-1-loan-default-prediction/data)
  
  

## Uses

- The data includes the names of the bank lending. It could be used to assess the relative performance of the banks from a lending perspective. 
- Is there anything about the composition of the dataset or the way it was collected and preprocessed/cleaned/labeled that might impact future uses? There is no information about the methods of data collection. 

## Distribution

- The datset is distributed on the Zindi website, but there is a restriction on its further use and distribution. It is subject to terms of use on the Zindi website.

## Maintenance

- The dataset is not a current dataset, it is purely for machine learning exercises, so in this respect it is not maintained. 

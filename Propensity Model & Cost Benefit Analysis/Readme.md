# Python Skillset :
- Data cleaning
- String manipulation
- Combine & merge datasets
- Data aggregation
- Descriptive statistic
- Analyzing using visualization
- Regression Analysis

## Revobank Propensity Model & Cost Benefit Analysis :
<a href="https://colab.research.google.com/drive/1PwxvxIwUFRp4a29qdqVl9gc_-5L4eRZ9?usp=sharing"> Google Colab </a>

## Situation

## Background
For 3 months between February and April 2023, the RevoBank Card Partnership Tribe has successfully implemented the installment feature or PayLater in Revoshop which aims to increase credit card usage. This service allows customers to convert e-commerce transactions into fixed installments with low interest rates.

## Problem Definition
As a success of this pilot program, the tribe leader plans Project Contact to 30,000 Revoshop customers who have never used the PayLater feature via phone call, offering a welcome bonus of 1000 reward points (worth 100 euros) if they activate and use PayLater for transactions.
As a data analyst, my role is to develop propensity models that predict which customers are most likely to use PayLater features. Then I can use the model to present a cost-benefit analysis of the project.

## Objective
The goal of this project is to build a propensity model to predict which customers are most likely to use PayLater features and perform a cost-benefit analysis to assess the potential impact of Project Contact.

## Task & Actions
- Import promotion data and Revobank paylater data into Google Colab	-> Use Python libraries including pandas and numpy	-> To load dataset and perform data cleaning

- Identify important columns that can be used for joining, create target variables and create new features ->	Use Python libraries including pandas, numpy, seaborn and matplotlib to analyze and visualize data	-> To prepare data for propensity model

- Build a model using train data and apply the trained model to the test dataset and evaluate performance	Use python libraries including LogisticRegression and XGBoost Classifier to build model	-> To train data, evaluate the model and identify the most promising pay-later customers

- Combine the model probability and the dataset (30,000 Revoshop customers who have never used the PayLater feature) ->	Use python libraries including LogisticRegression and XGBoost Classifier to build model ->	To apply the model to calculate the probability of customers using the pay-later

- Utilize the benefit-cost analysis template	-> Use spreadsheets	-> To assess the potential impact of project contact

## Result
The result of this project as follows:

- The **XGBoost Classifier** model is quite effective for identifying promising PayLater customers, shown by the High Precision and Decile-Based performance results. However, there is still room for improvement, especially in increasing the actual positive class to improve Recall
- The model estimates that an average probability of about **58%** of Revoshop's 30,000 customers will activate the PayLater feature. The following is a calculation of the potential impact :
    1. **Expected Revenue** : The projected revenue from selected top 30,000 customers are estimated 64,978,841 euros
    2. **Total Cost** : The total cost of implementing Project Contact is 26,231,700 euros including Cost of contacting customers (12,375 euros), Cost of contacting customers and delivery (29,325 euros) and Cost of welcome bonus (261,190,000 euros)
    3. **Return of Effort (R/E)** : The R/E ratio is calculated by dividing Expected Revenue by Total Costs, the result is 2.48
- An R/E value of **2.48** indicates that the potential financial benefits (expected income) from Project Contact are 2.48 times higher than the total costs incurred for the effort. This implies that the project is expected to be financially successful, generating a positive return on investment

# Deck
<a href="https://drive.google.com/file/d/1DfJyNasWAwlHIxXWPFv3dprj182D9naj/view?usp=share_link"> Propensity Model & Cost Benefit Analysis</a>

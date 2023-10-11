# Python Skillset :
- Data cleaning
- String manipulation
- Combine & merge datasets
- Data aggregation
- Descriptive statistic
- Analyzing using visualization
- Cluster Analysis

## RevoBank - Customer Segmentation using K-Means Clustering :
<a href="https://colab.research.google.com/drive/1P4hUoBLUAkVYsrR3NeUQJ6xxGOmBL9V2?usp=sharing"> Google Colab </a>

## Situation

## Background
RevoBank, a European bank that provides credit cards to its customers.
Over the last 6 months, Revo bank has implemented new promotions specifically for credit users. This promotion takes the form of distributing Revoshop vouchers, which is one of Revo Bank's partners, to all Revo Bank customers via email and SMS. Customers will receive 15 points equivalent to 1.5 euros for each voucher exchange for eligible transactions. As a data analyst, my role is to provide insight into promo performance in the past 6 months, create customer segmentation and identify business opportunities associated with the customer segmentation.

## Problem Definition
When customers are enrolled in a loyalty program, they tend to spend more money on each purchase, because they are incentivized to earn rewards. This increase in spending can lead to a significant increase in revenue for the business. Therefore, after running the promotion for 6 months, the Card Partnership Lead at Revo bank wanted to know spending patterns among Revoshop customers who used Revobank credit cards and looked for ways to reduce promotional costs.

## Objective
The aim of this project is to provide insight into promo performance in the last 6 months, create customer segmentation and identify business opportunities related to customer segmentation.

## Task & Actions
- Import dataset into Google Colab ->	Use Python libraries including pandas and numpy ->	To load dataset and perform data cleaning

- Identify dataset -> Use Python libraries including pandas, numpy, seaborn and matplotlib to analyze and visualize data	-> To analyze trends and pattern in promo performance in the last 6 months

- Create KMeans Clustering ->	Use Python libraries including KMeans, SilhouetteVisualizer	-> To find the segments of customers based on their promo sensitivity and potential to generate revenue

## Result
The result of this project, 3 clusters were obtained, namely Satisfied High Shoppers, Moderate Shoppers, and Cautious Shoppers. Based on these findings, 

- **Business Opportunity related to Cluster**

There are 3 clusters, where **Moderate Spenders** is a cluster that brings many benefits to Revobank. This cluster will **most likely provide more revenue** to Revobank with higher generated income, greater proportion sensitive to promos and **low promotional costs**

- **Target Female customers**

Female customers have a **significant impact on revenue** since they dominate transactions. RevoShop can increase engagement and drive higher spending among this segment

- **Emphasize SMS communication**

The analysis results show that promotions via SMS have a positive effect on customer engagement. RevoShop should allocate more efforts towards **sms campaigns to attract customer attention**. So it can lead to increased responses and purchases at RevoShop

# Deck
<a href="https://drive.google.com/file/d/1qyLEh7ffM89JBqP5BqNBcGRthj4HR8Yf/view?usp=share_link"> KMeans Clustering</a>

# SQL Skill sets:
- Standard Query Syntax
- SQL Aggregate Functions;
- SQL Window Function
- CTE

## TheLook E-Commerce Analysis

## Situation

### Background
The fashion e-commerce company is currently in the optimization mode due to the potential crisis in 2023. Therefore, management decided to cut resources in several categories with the lowest growth in the last 1 year. As a data analyst supporting the business, my role is to analyze retention cohort based on customer purchases and identify monthly inventory growth to provide actionable insights to management to make data-driven decisions

### Problem Definition
The potential crisis in 2023 is a major concern for many industries including fashion e-commerce companies because it will have a negative impact on their income and production. A crisis can lead to a decrease in revenue due to a decrease in consumption expenditure and customer retention. This can also harm the company's inventory growth by decreasing production quantities. Therefore, it is important for companies to identify which resource categories will have the lowest growth in 2022 to be immune from a potential crisis.

### Objective
The goal of this project is to identify monthly inventory growth trends and measure customer retention

### Task & Actions
- Collect inventory data -> Collect inventory data from Google BigQuery -> To identify trends and pattern in growth of inventory
  
- Identify inventory data -> Use SQL Advance (CTE, Window Function) to get monthly inventory growth in each product category -> To identify which product category has lowest growth

- Collect order data -> Collect order data from Google BigQuery -> To determine what data are needed for cohort analysis

- Create monthly retention cohort -> Use SQL Advance (CTE, Window Function) to create monthly retention cohort -> To measure customer retention based on their behavior and find out whether user engagement is actually getting better over time or just appearing to increase due to growth

### Result

The result of this project is that there are seasonal and non-seasonal product categories based on customer behavior, where Active Products, Socks & Hosiery, and Underwear have the lowest average inventory growth, so these products can be considered for the disconnected resource category. Then customers who start buying products in the winter have a lower retention rate than those who start in the summer.

Based on these findings, marketing teams need to improve user experience, offer incentives to encourage users to return, or adjust marketing strategies to target specific groups. And for further analysis it is necessary to carry out analysis including identifying the key factors that contribute to the negative monthly inventory growth rate which shows the inventory level has decreased during that month and to find out what variables influence the monthly inventory growth rate.

As a data analyst, I provide recommendations that help management make data-driven decisions to improve the company's business performance

## Deck
<a href="https://drive.google.com/file/d/1sh7g-aYHkK80zTlfhqZdGR3Fav-RSpwt/view?usp=sharing"> Cohort Analysis</a>

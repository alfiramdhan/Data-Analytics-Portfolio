# EDA
## 1. Total orders : 124,879
```SQL
SELECT COUNT(order_id)as total_order
FROM `sql-project-376612.thelook_ecommerce.orders`
```

## 2. Total complete order : 31,234
```sql
SELECT COUNT(order_id)as total_order
FROM `sql-project-376612.thelook_ecommerce.orders`
WHERE status = 'Complete';
```

## 3. Total calcelled order : 18,759
```sql
SELECT COUNT(order_id)as total_order
FROM `sql-project-376612.thelook_ecommerce.orders`
WHERE status = 'Cancelled'
```

## 4. Considering completed orders and focusing on the month of shipment, which month in the year 2021 had the lowest total order performance for the Jeans category?
```sql
SELECT
       DATE_TRUNC(date(o.shipped_at),month) as month,
       COUNT(o.order_id)as total_order
FROM sql-project-376612.thelook_ecommerce.orders o
LEFT JOIN sql-project-376612.thelook_ecommerce.order_items oi
         ON o.order_id = oi.order_id
LEFT JOIN sql-project-376612.thelook_ecommerce.products p
         ON oi.product_id = p.id
WHERE o.status = 'Complete'
         and EXTRACT(YEAR FROM o.shipped_at) = 2021
           and p.category = 'Jeans'
GROUP BY 1 
ORDER BY 2 ASC
LIMIT 1;
```

## 5. To retrieve the location with the highest number of buyers (use unique user) who made purchases on our platform during the year 2022, which of the following SQL scripts is correct?
```sql
SELECT u.country,
        COUNT(DISTINCT o.user_id)as number_buyers
FROM sql-project-376612.thelook_ecommerce.users u
LEFT JOIN sql-project-376612.thelook_ecommerce.orders o
        ON u.id = o.user_id
WHERE EXTRACT(YEAR FROM o.shipped_at) = 2022
        AND o.status = 'Complete'
GROUP BY 1
ORDER BY 2 DESC
LIMIT 1;
```

## 6. Considering the completed orders that were shipped in the year 2022,
which distribution center to which country destination had the highest total number of items sold?
```sql
SELECT dc.name,
        u.country,
        SUM(o.num_of_item)as total_item_sold
FROM sql-project-376612.thelook_ecommerce.orders o
LEFT JOIN sql-project-376612.thelook_ecommerce.users u
  ON o.user_id = u.id
LEFT JOIN sql-project-376612.thelook_ecommerce.order_items oi
  ON o.order_id = oi.order_id
LEFT JOIN sql-project-376612.thelook_ecommerce.products p
  ON oi.product_id = p.id
LEFT JOIN sql-project-376612.thelook_ecommerce.distribution_centers dc
  ON p.distribution_center_id = dc.id
WHERE o.status = 'Complete'
  AND EXTRACT(YEAR FROM o.shipped_at) = 2022
GROUP BY 1,2
ORDER BY 3 DESC
LIMIT 1;
```

----
## 1. How is the monthly inventory growth trend in percentage by product category in the past 1 year?

### Steps 1 :
- Create `CTE` to break up complex queries in BigQuery
- In first table, we can calculate number of event in inventory in each month each category
- Use `DATE_TRUNC()` to truncates a month value
- Use `COUNT DISTINCT` to remove duplicate
- Use `EXTRACT()` to extracts part of a year from a DATE value

```sql
WITH current_inventory AS(
SELECT
       DATE_TRUNC(date(created_at),month) as month,
       product_category,
       COUNT(DISTINCT id)as number_inventory
FROM
       sql-project-376612.thelook_ecommerce.inventory_items

WHERE
      EXTRACT(YEAR FROM date(created_at)) = 2022
GROUP BY
      1,2
),
```

### Steps 2 :
- In second table. we get the previous number of event in inventory in each month each category
- Use window function `LAG()` to get a value of `number_inventory` for a preceding row.
- Use `OVER (PARTITION BY)` to break `product_category` into separate sections (partitions) by ordering current_inventory in ascending

```sql
prev_inventory AS(
SELECT
      month,
      product_category,
      number_inventory,
      LAG(number_inventory)
      OVER(PARTITION BY product_category ORDER BY current_inventory.month) as number_inventory_prev
FROM
    	Current_inventory
)
```

### Then we can get the monthly growth of inventory by dividing number_inventory by number_inventory_prev from `prev_inventory` table

```sql
SELECT *,
      ROUND((number_inventory/number_inventory_prev) -1,2) as monthly_growth

FROM
      prev_inventory
ORDER BY
      product_category, month desc;
```
----

## 2. How is the monthly user retention in the past 1 year?

### Steps 1 :
- Create `CTE` to break up complex queries in BigQuery
- In first table, we can get the minimum (earliest) truncated month value for each user_id group with the following,
- Use `DATE()` to extracts the date portion from the created_at column
- Use `DATE_TRUNC(DATE(created_at), MONTH)` to truncates the date to the beginning of the month
- Use `MIN(...)` to calculate the minimum value of the expression within the specified window frame
- Then use `OVER(PARTITION BY user_id)` to define the window frame for the window function. It partitions the data by the user_id column, creating separate groups for each unique user_id

```sql
WITH user_activity AS(
 SELECT
      DISTINCT user_id,
       MIN(DATE_TRUNC(DATE(created_at),MONTH)) OVER(PARTITION BY user_id) as first_order_date,
       DATE_TRUNC(DATE(created_at),MONTH)as running_order_date
 FROM
       `sql-project-376612.thelook_ecommerce.orders`   
WHERE
       status = 'Complete'
            AND EXTRACT(YEAR FROM DATE(created_at)) = 2022
),
```

## Step 2 :
- In second table, we can number of unique customer for each first_order_date group with the following,
- Use `DATE_DIFF()` to get the difference month
- Use `COUNT(DISTINCT user_id)` to calculate number of unique customer
- Use `OVER(PARTITION BY first_order_date)` to define the window frame for the window function. It partitions the data by the user_id column, creating separate groups for each unique user_id

```sql
cohort_sizes AS(
 SELECT *,
       DATE_DIFF(running_order_date, first_order_date,month) as diff_month,
       COUNT(DISTINCT user_id) OVER(PARTITION BY first_order_date) cohort_size
 FROM
       user_activity     
),
```

## Step 3 :
- In third table, we can get the number of customer retention by counting number of unique customer

```sql
retention_table AS(
 SELECT
       first_order_date,
       diff_month,
       cohort_size,
       COUNT(DISTINCT user_id)as number_user
 FROM cohort_sizes     
 GROUP BY 1,2,3
 ORDER BY 1,2
)
 SELECT *,
         number_user / cohort_size as pct
 FROM retention_table;
```
----

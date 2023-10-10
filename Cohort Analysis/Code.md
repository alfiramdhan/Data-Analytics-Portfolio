# 1. How is the monthly inventory growth trend in percentage by product category in the past 1 year?

## Steps 1 :
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

## Steps 2 :
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

## Then we can get the monthly growth of inventory by dividing number_inventory by number_inventory_prev from `prev_inventory` table

```sql
SELECT *,
      ROUND((number_inventory/number_inventory_prev) -1,2) as monthly_growth

FROM
      prev_inventory
ORDER BY
      product_category, month desc;
```

# 2. How is the monthly user retention in the past 1 year?
```sql
WITH user_activity AS(
 SELECT
      DISTINCT user_id,
       MIN(DATE_TRUNC(DATE(created_at),MONTH))
OVER(PARTITION BY user_id) as first_order_date,
       DATE_TRUNC(DATE(created_at),MONTH)as running_order_date
 FROM `sql-project-376612.thelook_ecommerce.orders`   
  WHERE status = 'Complete'
     AND EXTRACT(YEAR FROM DATE(created_at)) = 2022
),

cohort_sizes AS(
 SELECT *,
       DATE_DIFF(running_order_date, first_order_date,month)as
diff_month,
       COUNT(DISTINCT user_id)
OVER(PARTITION BY first_order_date) cohort_size
 FROM user_activity     
),
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

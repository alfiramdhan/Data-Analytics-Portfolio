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

SELECT *,
      ROUND((number_inventory/number_inventory_prev) -1,2) as monthly_growth

FROM
      prev_inventory
ORDER BY
      product_category, month desc;
```

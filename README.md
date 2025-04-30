
1. Understanding the Task
You want to:
•  Explore customer ordering behavior
•  Identify repeat ordering patterns
•  Segment customers (e.g., by order frequency or spending)
•  Analyze trends over time
________________________________________
2. Planning the SQL Queries
Key metrics to include:
•  Number of orders per customer (to find repeat customers)
•  Total amount spent per customer (for segmentation)
•  First and last order dates (to analyze customer lifecycle)
•  Orders per customer over time (to see trends)
________________________________________
3. Example SQL Queries
a) Customer Order Summary
SELECT
  customer_id,
  COUNT(order_id) AS total_orders,
  SUM(order_amount) AS total_spent,
  MIN(order_date) AS first_order_date,
  MAX(order_date) AS last_order_date
FROM
  customer_orders
GROUP BY
  customer_id
ORDER BY
  total_orders DESC;
This query helps you identify repeat customers and segment them by order count and spending.
________________________________________
b) Repeat vs. One-time Customers
WITH customer_counts AS (
  SELECT customer_id, COUNT(order_id) AS total_orders
  FROM customer_orders
  GROUP BY customer_id
)
SELECT
  CASE
    WHEN total_orders = 1 THEN 'One-time'
    ELSE 'Repeat'
  END AS customer_type,
  COUNT(*) AS num_customers
FROM customer_counts
GROUP BY customer_type;
This query segments your customers into one-time and repeat buyers.
________________________________________
c) Customer Ordering Trends Over Time
   
SELECT
  DATE_TRUNC ('month', order_date) AS month,
  COUNT(DISTINCT customer_id) AS active_customers,
  COUNT(order_id) AS total_orders
FROM
  customer_orders
GROUP BY
  DATE_TRUNC ('month', order_date)
ORDER BY
  month;
This query shows how many customers and orders you have each month, revealing trends over time.
________________________________________

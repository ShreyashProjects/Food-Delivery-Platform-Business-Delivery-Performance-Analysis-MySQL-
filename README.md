# Food-Delivery-Platform-Business-Delivery-Performance-Analysis-MySQL-
# Food Delivery Platform – Business & Delivery Performance Analysis (MySQL)

## Project Overview

This project analyzes a food delivery platform dataset similar to services like Swiggy or Zomato.

The goal of the project is to extract meaningful business insights using SQL queries related to:

- Customer ordering behavior
- Restaurant performance
- Delivery efficiency
- Revenue analysis
- Peak ordering hours

This project demonstrates how SQL can be used for real-world business data analysis.

--------------------------------------------------

## Database Tables

1. customers
2. restaurants
3. delivery_agents
4. orders
5. order_items

--------------------------------------------------

## SQL Analysis Queries

### 1 Total Number of Orders

SELECT COUNT(*) AS total_orders
FROM orders;

--------------------------------------------------

### 2 Total Revenue Generated

SELECT SUM(order_amount) AS total_revenue
FROM orders
WHERE order_status = 'Delivered';

--------------------------------------------------

### 3 Average Order Value

SELECT AVG(order_amount) AS avg_order_value
FROM orders
WHERE order_status = 'Delivered';

--------------------------------------------------

### 4 Top 5 Customers by Spending

SELECT 
c.customer_id,
c.name,
SUM(o.order_amount) AS total_spent
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.name
ORDER BY total_spent DESC
LIMIT 5;

--------------------------------------------------

### 5 Customers Who Ordered More Than 3 Times

SELECT 
c.customer_id,
c.name,
COUNT(o.order_id) AS total_orders
FROM customers c
JOIN orders o
ON c.customer_id = o.customer_id
GROUP BY c.customer_id, c.name
HAVING COUNT(o.order_id) > 3;

--------------------------------------------------

### 6 Customer Type Distribution

SELECT 
customer_type,
COUNT(*) AS total_customers
FROM customers
GROUP BY customer_type;

--------------------------------------------------

### 7 Top Performing Restaurant by Revenue

SELECT 
r.restaurant_name,
SUM(o.order_amount) AS total_revenue
FROM restaurants r
JOIN orders o
ON r.restaurant_id = o.restaurant_id
GROUP BY r.restaurant_name
ORDER BY total_revenue DESC
LIMIT 1;

--------------------------------------------------

### 8 Average Restaurant Rating by City

SELECT 
city,
AVG(rating) AS avg_rating
FROM restaurants
GROUP BY city;

--------------------------------------------------

### 9 Most Ordered Cuisine Type

SELECT 
r.cuisine,
COUNT(o.order_id) AS total_orders
FROM restaurants r
JOIN orders o
ON r.restaurant_id = o.restaurant_id
GROUP BY r.cuisine
ORDER BY total_orders DESC
LIMIT 1;

--------------------------------------------------

### 10 Average Delivery Time by City

SELECT 
r.city,
AVG(TIMESTAMPDIFF(MINUTE, o.order_time, o.delivery_time)) AS avg_delivery_time
FROM orders o
JOIN restaurants r
ON o.restaurant_id = r.restaurant_id
GROUP BY r.city;

--------------------------------------------------

### 11 Fastest Delivery Agents

SELECT 
d.agent_name,
AVG(TIMESTAMPDIFF(MINUTE, o.order_time, o.delivery_time)) AS avg_delivery_time
FROM delivery_agents d
JOIN orders o
ON d.agent_id = o.agent_id
GROUP BY d.agent_name
ORDER BY avg_delivery_time ASC;

--------------------------------------------------

### 12 Delayed Orders

SELECT 
order_id,
customer_id,
order_time,
delivery_time
FROM orders
WHERE order_status = 'Delayed';

--------------------------------------------------

### 13 Peak Order Hour

SELECT 
HOUR(order_time) AS order_hour,
COUNT(*) AS total_orders
FROM orders
GROUP BY order_hour
ORDER BY total_orders DESC;

--------------------------------------------------

### 14 Orders Per Day

SELECT 
DATE(order_time) AS order_date,
COUNT(*) AS total_orders
FROM orders
GROUP BY order_date
ORDER BY order_date;

--------------------------------------------------

### 15 Monthly Revenue Trend

SELECT 
YEAR(order_time) AS year,
MONTH(order_time) AS month,
SUM(order_amount) AS total_revenue
FROM orders
WHERE order_status = 'Delivered'
GROUP BY year, month
ORDER BY year, month;

--------------------------------------------------

## Skills Demonstrated

- SQL Joins
- Aggregation Functions
- Group By
- Subqueries
- Date Functions
- Business Data Analysis

--------------------------------------------------

## Tools Used

- MySQL
- SQL
- GitHub

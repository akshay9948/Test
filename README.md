
# PIZZA SALES

SQL QUERIES

A. KPI’s
1. Total Revenue:
SELECT SUM(total_price) AS Total_Revenue
FROM pizza_sales;

![image](https://github.com/akshay9948/Test/assets/159958301/b1904761-a0a0-4729-b1e9-553a39b7b371)

 
2. Average Order Value:
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value
FROM pizza_sales;

![image](https://github.com/akshay9948/Test/assets/159958301/ff1babab-f140-4276-9c60-971d2a5a968c)

 
3. Total Pizzas Sold:
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;

![image](https://github.com/akshay9948/Test/assets/159958301/6f1dcea1-3e0c-4d29-8217-29749cd10864)
 
4. Total Orders:
SELECT COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales;

![image](https://github.com/akshay9948/Test/assets/159958301/21a3a1d2-326b-4580-b17f-1bc502aebf8c)
 
5. Average Pizzas Per Order:
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales;

![image](https://github.com/akshay9948/Test/assets/159958301/e4a24fee-4996-4569-bece-ab230164c995)
 
B. Daily Trend for Total Orders:

SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date)

Output:
 
![image](https://github.com/akshay9948/Test/assets/159958301/78a798ff-0f42-4789-b9b8-42f4bddd9a51)

C. Monthly Trend for Orders:

select DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
from pizza_sales
GROUP BY DATENAME(MONTH, order_date)

Output:

![image](https://github.com/akshay9948/Test/assets/159958301/4323a414-3e98-412e-805a-315859dcb7ab)


D. % of Sales by Pizza Category:

SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category

Output:

![image](https://github.com/akshay9948/Test/assets/159958301/328a3101-44fb-4e49-89f4-9bace56db2a1)
 
E. % of Sales by Pizza Size:

SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size

Output:

![image](https://github.com/akshay9948/Test/assets/159958301/1bfc662d-939c-4ee7-9b49-11099d0dded9)
 
F. Total Pizzas Sold by Pizza Category:

SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC

Output:

![image](https://github.com/akshay9948/Test/assets/159958301/ecb70fea-1de3-429c-88d2-1b83128c3e54)
 
G. Top 5 Pizzas by Revenue:

SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC

![image](https://github.com/akshay9948/Test/assets/159958301/60fbf803-0fa8-4a24-a604-2a0277a5a163)
 
H. Bottom 5 Pizzas by Revenue:

SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC

![image](https://github.com/akshay9948/Test/assets/159958301/6b97bc7c-9427-4bf5-b3c8-1f6b000876e4)
 
I. Top 5 Pizzas by Quantity:

SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC

Output

![image](https://github.com/akshay9948/Test/assets/159958301/c6693ff3-b491-4e52-84de-5370bd0f1d05)
 
J. Bottom 5 Pizzas by Quantity
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC
Output
 
![image](https://github.com/akshay9948/Test/assets/159958301/5d2dec75-dbc1-482d-b20a-037929dbe31e)


K. Top 5 Pizzas by Total Orders:

SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC

![image](https://github.com/akshay9948/Test/assets/159958301/fe434a71-e3c2-4c90-99f9-7fc9bc806ab8)
 
L. Borrom 5 Pizzas by Total Orders:

SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC

![image](https://github.com/akshay9948/Test/assets/159958301/6dcc36ae-5d2a-4f83-b491-824a7677d452)
 
NOTE:

If you want to apply the pizza_category or pizza_size filters to the above queries you can use WHERE clause. Follow some of below examples
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
WHERE pizza_category = 'Classic'
GROUP BY pizza_name
ORDER BY Total_Orders ASC


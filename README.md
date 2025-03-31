# retail-sales-analysis
This project analyzes customer purchase behavior, sales trends, and product performance using MySQL
# Retail Sales Analysis 📊

## 📌 Project Overview
This project analyzes retail sales data to uncover insights on customer behavior, sales performance, and product trends using MySQL.

## 🔍 Key Insights
- 🛍 **Top Customers**: Identified highest spending customers.
- 📈 **Sales Trends**: Monthly and yearly revenue patterns.
- 🏆 **Best-Selling Products**: Products with the highest revenue and quantity sold.
- 🌍 **Geographical Analysis**: Sales distribution by customer location.

## 🗂 Dataset
- **Customers**: Contains customer demographics.
- **Products**: List of products with prices.
- **Sales**: Transaction history.

## 🗂 **Dataset Structure**
### 1️⃣ **Customers Table**
| Column Name  | Data Type  | Description |
|-------------|-----------|-------------|
| customer_id | INT       | Unique customer identifier |
| name        | VARCHAR   | Customer name |
| gender      | VARCHAR   | Customer gender (Male/Female) |
| age         | INT       | Customer age |
| location    | VARCHAR   | Customer's city or region |
| signup_date | DATE      | Date when the customer signed up |

### 2️⃣ **Products Table**
| Column Name  | Data Type  | Description |
|-------------|-----------|-------------|
| product_id  | INT       | Unique product identifier |
| product_name | VARCHAR  | Name of the product |
| category    | VARCHAR   | Product category |
| price       | DECIMAL   | Product price |
| supplier    | VARCHAR   | Supplier name |

### 3️⃣ **Sales Table**
| Column Name  | Data Type  | Description |
|-------------|-----------|-------------|
| sale_id     | INT       | Unique sale transaction ID |
| customer_id | INT       | Customer who made the purchase |
| product_id  | INT       | Product purchased |
| quantity    | INT       | Number of units bought |
| total_price | DECIMAL   | Total price of the sale (quantity * price) |
| purchase_date | DATE    | Date of the transaction |
| payment_method | VARCHAR | Payment method used |

## 🛠 SQL Queries

### Customer Segmentation

### 1️⃣ Find top 10 customers BY total spending.
```sql
SELECT c.customer_id,
       c.name,
       Sum(s.total_price) AS total_spending
FROM customers c
INNER JOIN sales s ON c.customer_id = s.customer_id
GROUP BY c.customer_id,
         c.name
ORDER BY total_spending DESC
LIMIT 10;
```

### 2️⃣ Count new customers per month.
```sql
SELECT date_format(signup_date, '%Y-%m') AS MONTH,
       count(customer_id)
FROM customers
GROUP BY MONTH
ORDER BY MONTH;
```

### 3️⃣ Find the average order value per customer.
```sql
SELECT c.customer_id,
       c.name Sum(s.quantity * p.price) / Count(DISTINCT s.sale_id) AS avg_order_value
FROM Sales s
INNER JOIN Customers c ON s.customer_id = c.customer_id
INNER JOIN Products p ON s.product_id = p.product_id
GROUP BY c.customer_id,
         c.name
ORDER BY avg_order_value DESC;
```

### Sales Performance 
### 1️⃣ Monthly and yearly revenue trends.
```sql
SELECT date_format(s.purchase_date, "%Y-%m") AS month_date,
       Sum(s.total_price)AS total_revenue
FROM sales s
GROUP BY month_date
ORDER BY month_date;
```

### 2️⃣ How many products were sold using each payment method?
```sql
SELECT distinct(s.payment_method),
       count(p.product_name)
FROM sales s
INNER JOIN products p ON p.product_id = s.product_id
GROUP BY s.payment_method;
```

### 3️⃣ Top suppliers with the highest revenue
``` sql
SELECT distinct(p.supplier),
       sum(s.total_price) AS total_revenue
FROM sales s
INNER JOIN products p ON p.product_id = s.product_id
GROUP BY p.supplier
ORDER BY total_revenue DESC
LIMIT 10;
```

### 4️⃣ Best-selling products BY revenue & quantity. 
#### BY Revenue:
```sql
SELECT p.product_id,
       p.product_name,
       Sum(s.total_price) AS total_revenue
FROM products p
INNER JOIN sales s ON p.product_id = s.product_id
GROUP BY p.product_id,
         p.product_name
ORDER BY total_revenue
LIMIT 10;
```

#### BY Quantity:
``` sql
SELECT p.product_id,
       p.product_name,
       Sum(s.quantity) AS total_quantity
FROM products p
INNER JOIN sales s ON p.product_id = s.product_id
GROUP BY p.product_id,
         p.product_name
ORDER BY total_quantity
LIMIT 10;
```

### Product Performance
### 1️⃣ Identify top 10 underperforming products.
```sql
SELECT p.product_id,
       p.product_name,
       sum(s.total_price) AS total_revenue
FROM products p
INNER JOIN sales s ON p.product_id = s.product_id
GROUP BY p.product_id,
         p.product_name
ORDER BY revenue ASC
LIMIT 10;
```

### 2️⃣ Which product category contributes the most to revenue.
```sql
SELECT p.category,
       sum(s.total_price) AS total_revenue
FROM products p
INNER JOIN sales s ON p.product_id = s.product_id
GROUP BY p.category
ORDER BY revenue DESC;
```

### 3️⃣ Average revenue per product category?
``` sql
SELECT p.category,
       avg(s.total_price) AS average_revenue
FROM products p
INNER JOIN sales s ON p.product_id = s.product_id
GROUP BY p.category 4. Geographical Insights • Sales distribution BY customer location.
SELECT c.location,
       sum(s.total_price) AS total_revenue
FROM customers c
INNER JOIN sales s ON c.customer_id = s.customer_id
GROUP BY c.location
ORDER BY total_revenue DESC;
```

### 4️⃣ Top-performing locations.
```sql
SELECT c.location,
       sum(s.total_price) AS total_revenue
FROM customers c
INNER JOIN sales s ON c.customer_id = s.customer_id
GROUP BY c.location
ORDER BY total_revenue DESC
LIMIT 10;
```


## 🔗 Connect with Me
📩 Email: phamthanhtu2609@gmail.com  
🔗 www.linkedin.com/in/thanh-tú-phạm-62899b225 

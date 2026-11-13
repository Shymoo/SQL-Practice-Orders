# README

# SQL Practice: Orders Analysis

A beginner-to-intermediate SQL project. It builds a database called `SQL_Practice`, creates an `Orders` table with 20 sample rows, and answers business questions using filtering, sorting, pattern matching and calculated expressions.

## Database Used

MySQL (tested in MySQL Workbench).

## Project Structure

```
SQL-Practice-Orders/
├── README.md
├── 01_create_database_and_table.sql
├── 02_insert_data.sql
├── 03_queries.sql
└── screenshots/
```

## How to Run

1. Run `01_create_database_and_table.sql` to create the database and table.
2. Run `02_insert_data.sql` to load the 20 rows.
3. Run `03_queries.sql` to execute the analysis queries.

## SQL Concepts Covered

- `CREATE DATABASE`, `CREATE TABLE`, `INSERT`
- `SELECT`, `WHERE`, `ORDER BY` (ASC and DESC)
- `AND`, `OR`, `IN`, `BETWEEN`, `LIKE`
- `DISTINCT`
- `IS NULL` and `IS NOT NULL`
- Calculated expressions such as `quantity * unit_price`

---

## Part 1: Database Setup

### 1. Build the database

```sql
DROP DATABASE IF EXISTS `SQL_Practice`;
CREATE DATABASE `SQL_Practice`;
USE `SQL_Practice`;
```

Create database

![Create database](README/Q1.png)

Create database

### 2. Build the Orders table with suitable data types and constraints

Create table

![Create table](README/Q2__Q3.png)

Create table

### 3. Insert the 20 rows

Insert data

![Insert data](README/Q4.png)

---

## Part 2: Basic Queries

### 1. Display all columns from the Orders table

```sql
SELECT *
FROM SQL_Practice.Orders;
```

Select all

![Select all](README/Q5.png)

### 2. Display only OrderID, CustomerID and Sales

```sql
SELECT order_id, customer_id, sales
FROM SQL_Practice.Orders;
```

Select columns

![Select columns](README/Screenshot_2026-11-13_at_19.55.27.png)

### 3. Show all orders where Sales > 500

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE sales > 500;
```

Sales over 500

![Sales over 500](README/Screenshot_2026-11-13_at_19.56.12.png)

### 4. Retrieve orders where Quantity = 1

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE quantity = 1;
```

Quantity equals 1

![Quantity equals 1](README/Screenshot_2026-11-13_at_19.56.33.png)

### 5. Display all orders where Country = ‘USA’

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE country = 'USA';
```

Country USA

![Country USA](README/Screenshot_2026-11-13_at_19.57.05.png)

### 6. List all distinct countries

```sql
SELECT DISTINCT country
FROM SQL_Practice.Orders;
```

Distinct countries

![Distinct countries](README/Screenshot_2026-11-13_at_19.57.25.png)

### 7. Show orders where Profit < 0

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE profit < 0;
```

Negative profit

![Negative profit](README/Screenshot_2026-11-13_at_19.57.46.png)

### 8. Retrieve orders where Discount >= 0.2

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE discount >= 0.2;
```

Discount 0.2 or more

![Discount 0.2 or more](README/Screenshot_2026-11-13_at_19.58.03.png)

### 9. Display orders where ShipDate IS NULL

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE ship_date IS NULL;
```

Unshipped orders

![Unshipped orders](README/Screenshot_2026-11-13_at_19.58.19.png)

---

## Part 3: Filtering, Sorting and Pattern Matching

### 1. Orders where Sales = Quantity * UnitPrice

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE sales = quantity * unit_price;
```

Sales equals quantity x price

![Sales equals quantity x price](README/Screenshot_2026-11-13_at_19.59.02.png)

### 2. Category is Furniture OR Technology

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE category = 'Furniture' OR category = 'Technology';
```

Furniture or technology

![Furniture or technology](README/Screenshot_2026-11-13_at_19.59.39.png)

### 3. CustomerID starts with ‘C’ (LIKE)

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE customer_id LIKE 'C%';
```

Customer starts with C

![Customer starts with C](README/Screenshot_2026-11-13_at_19.59.57.png)

### 4. Orders placed in 2023 (BETWEEN)

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE order_date BETWEEN '2023-01-01' AND '2023-12-31';
```

![Orders in 2023](README/Screenshot_2026-11-13_at_20.00.16.png)

### 5. Sales > 500 AND Profit > 0, ordered by Profit

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE sales > 500 AND profit > 0
ORDER BY profit;
```

Sales and profit ordered

![Sales and profit ordered](README/Screenshot_2026-11-13_at_20.00.51.png)

### 6. Country IN (USA, UK, Germany), ordered by Sales DESC

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE country IN ('USA', 'UK', 'Germany')
ORDER BY sales DESC;
```

### 7. Discount is not NULL and greater than 0, sorted by Discount ASC

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE discount IS NOT NULL AND discount > 0
ORDER BY discount ASC;
```

### 8. (Quantity * UnitPrice) - Discount > 1000

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE (quantity * unit_price) - discount > 1000;
```

### 9. Product name contains ‘Chair’ AND Sales BETWEEN 200 AND 1000

```sql
SELECT *
FROM SQL_Practice.Orders
WHERE product_name LIKE '%Chair%'
  AND sales BETWEEN 200 AND 1000;
```

### 10. Distinct CustomerID where Country = ‘USA’ AND Profit < 0, ordered alphabetically

```sql
SELECT DISTINCT customer_id
FROM SQL_Practice.Orders
WHERE country = 'USA' AND profit < 0
ORDER BY customer_id;
```

---

## Key Learnings

- **NULL needs `IS NULL`.** `= NULL` runs without an error but returns 0 rows, because NULL means unknown and nothing equals unknown.
- **Wildcard position matters.** `LIKE '%Chair%'` finds the word anywhere. `'%Chair'` finds it only at the end and misses “desk chair pro”.
- **`BETWEEN` is inclusive** of both end values, and the smaller value must come first.
- **Case sensitivity differs by database.** Data is stored in lowercase (`'usa'`). MySQL and SQL Server match `'USA'` by default, but PostgreSQL does not. Use `LOWER(country) = 'usa'` to be portable.
- **Choose column sizes from the real data.** `VARCHAR(10)` is too short for `'conference chair'`, so product names use `VARCHAR(100)`.
- **Use `DECIMAL` for money**, not `FLOAT`, to avoid rounding errors.
- **Don’t duplicate stored data.** `sales` already equals `quantity * unit_price`, so a second column for it would be redundant.
- **Ties in `ORDER BY` are not guaranteed to be in a fixed order.** Add a second sort column such as `order_id` for consistent output.

Shaima Aser [LinkedIn](https://www.linkedin.com/in/shaimaabd/) | [GitHub](https://github.com/your-username)

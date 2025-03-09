# Ejercicios-SQL
Ejercicios de Laboratorio
# Soluciones a las Prácticas de DataLemur

## Basic SQL

### Lección 102
#### Práctica 1 - SQL Select Practice Exercise
```sql
SELECT product_id, product_category, product_name FROM products
```
### Lección 103
#### Práctica 2 - WHERE Practice Exercise
```sql
SELECT user_id,stars 
FROM reviews
WHERE stars=3;
```
### Lección 104
#### Práctica 3 - SQL WHERE AND Practice Exercise
```sql
SELECT *
FROM reviews
WHERE stars > 3 
  AND review_id < 6000
  AND review_id >2000
  AND user_id != 142;
```

#### Práctica 4 - SQL AND OR Practice Exercise
```sql
SELECT * 
FROM reviews
WHERE (stars > 2 AND stars <= 4) 
  AND (user_id = 123
  OR user_id = 265
  OR user_id = 362);
```
### Lección 105
#### Práctica 5 - SQL BETWEEN Practice Exercise
```sql
SELECT manufacturer, drug, units_sold 
FROM pharmacy_sales
WHERE (manufacturer = 'AbbVie'
  OR manufacturer = 'Biogen'
  OR manufacturer = 'Eli Lilly')
  AND units_sold BETWEEN 100000 AND 105000;
```
### Lección 106
#### Práctica 6 - SQL IN Practice Exercise
```sql
SELECT manufacturer, drug, units_sold
FROM pharmacy_sales
WHERE manufacturer IN('Roche','Bayer','AstraZeneca') 
 AND units_sold NOT BETWEEN 55000 AND 550000;
```
### Lección 107
#### Prácticas 7 - SQL LIKE % Practice
```sql
SELECT * 
FROM customers 
WHERE customer_name LIKE 'F%ck';
```

#### Práctica 8 - SQL LIKE _ Practice
```sql
SELECT * 
FROM customers 
WHERE customer_name LIKE '_ee%';
```
### Lección 108
#### Práctica 9 - SQL Filtering Practice Exercise #1
```sql
SELECT * 
FROM customers 
WHERE age BETWEEN 18 AND 22
  AND state IN('Victoria','Tasmania','Queensland')
  AND gender !='n/a'
  AND (customer_name LIKE 'A%' OR customer_name LIKE 'B%');
```
## Intermediate SQL

### Lección 202
#### Práctica 1 - SQL COUNT Practice Exercise
```sql
SELECT COUNT(*) 
FROM pharmacy_sales;
```
#### Práctica 2 - SQL SUM Practice Exercise
```sql
SELECT COUNT(manufacturer), SUM(total_sales) 
FROM pharmacy_sales
WHERE manufacturer='Pfizer';
```
#### Práctica 3 - SQL AVG Practice Exercise
```sql
SELECT AVG(open) 
FROM stock_prices
WHERE ticker='GOOG';
```
#### Práctica 4 - SQL MIN Practice Exercise: Microsoft Stock
```sql
SELECT MIN(open) 
FROM stock_prices
WHERE ticker='MSFT';
```
#### Práctica 5 - SQL MAX Practice Exercise: Tesla Stock
```sql
SELECT MAX(open) 
FROM stock_prices
WHERE ticker='NFLX';
```

### Lección 203
#### Práctica 6 - GROUP BY Practice Exercise #1
```sql
SELECT ticker,MIN(open)
FROM stock_prices
GROUP BY ticker
ORDER BY MIN(open) DESC
```
#### Práctica 7 - GROUP BY Practice Exercise #2
```sql
SELECT skill,COUNT(candidate_id) 
FROM candidates
GROUP BY skill
ORDER BY COUNT(candidate_id) DESC;
```

### Lección 204
#### Práctica 8 - SQL HAVING MIN Practice Exercise
```sql
SELECT ticker,MIN(open)
FROM stock_prices
GROUP BY ticker
HAVING MIN(open)>100;
```
#### Práctica 9 - SQL HAVING Practice Exercise #2
```sql
SELECT candidate_id
FROM candidates
GROUP BY candidate_id
HAVING COUNT(skill)>2;
```

### Lección 205
#### Práctica 10 - SQL COUNT DISTINCT Practice Exercise
```sql
SELECT category, COUNT(DISTINCT product)
FROM product_spend
GROUP BY category;
```
### Lección 206
#### Práctica 11 - Practice SQL Subtraction: CVS Pharmacy Interview Question
```sql
SELECT drug, total_sales-cogs AS total_profit
FROM pharmacy_sales
GROUP BY drug,total_profit
ORDER BY total_profit DESC
LIMIT 3
```
#### Práctica 12 - Practice SQL Arithmetic: JPMorgan Chase SQL Interview Question
```sql
SELECT card_name, MAX(issued_amount)-MIN(issued_amount) AS difference
FROM monthly_cards_issued
GROUP BY card_name
ORDER BY difference DESC;
```
#### Práctica 13 - SQL Math Practice Exercise: Big-Mover Months
```sql
SELECT ticker, COUNT(ticker)
FROM stock_prices
WHERE ((close - open)*100)/open > 10 OR ((close - open)*100)/open < -10
GROUP BY ticker
ORDER BY count DESC;
```

### Lección 207
#### Práctica 14 - SQL CEIL Practice Exercise
```sql
SELECT drug, CEIL(total_sales/units_sold) AS unit_cost
FROM pharmacy_sales
WHERE manufacturer = 'Merck'
ORDER BY unit_cost;
```
### Lección 208
#### Práctica 15 - Google SQL Interview Question Using Division & Casting
```sql
Ejercicio bloqueado (requiere suscripción premiun)
```
### Lección 209
#### Práctica 16 - Tesla Null SQL Interview Question
```sql
SELECT part, assembly_step
FROM parts_assembly
WHERE finish_date IS NULL;
```
### Lección 210
#### Práctica 17 - Using CASE-ELSE Clause with CASE Statement in SELECT Statement
```sql
SELECT actor,character,platform, avg_likes,
CASE 
  WHEN avg_likes >= 15000 THEN 'Super Likes'
  WHEN avg_likes BETWEEN 5000 AND 14999 THEN 'Good Likes'
  ELSE 'Low Likes'
  END AS likes_category
FROM marvel_avengers
ORDER BY avg_likes DESC;
```
#### Práctica 18 - NYT SQL Interview Question: Laptop vs. Mobile Viewership
```sql
SELECT 
  COUNT(CASE 
    WHEN device_type='laptop' THEN 1
    ELSE NULL
  END) AS laptop_views
  ,COUNT(CASE 
    WHEN device_type IN('tablet','phone') THEN 1
    ELSE NULL
  END) AS mobile_views
FROM viewership;
```

### Lección 211
#### Práctica 19 - Easy SQL JOIN Practice Exercise
```sql
SELECT * 
FROM trades
JOIN users
  ON trades.user_id = users.user_id;
```
#### Práctica 20 - Harder SQL Join Interview Question
```sql
SELECT  city, COUNT(order_id)
FROM trades
JOIN users
  ON trades.user_id = users.user_id
WHERE status = 'Completed'
GROUP BY city
ORDER BY COUNT(order_id) DESC
LIMIT 3
```
#### Práctica 21 - Handling Nulls + JOIN SQL Interview Question
```sql
SELECT page_id 
FROM pages
WHERE page_id NOT IN (SELECT DISTINCT(page_id) FROM page_likes);
```

### Lección 212
#### Práctica 22 - Extracting Parts from Dates in SQL
```sql
SELECT user_id,
  EXTRACT(DAYS FROM (MAX(post_date) - MIN(post_date))) AS days_between
FROM posts
WHERE EXTRACT(YEAR FROM post_date) = '2021'
GROUP BY 1
HAVING COUNT(post_id) > 1
ORDER BY user_id;
```
#### Práctica 23 - Adding and Subtracting Intervals in SQL
```sql
SELECT DISTINCT user_id
FROM emails 
INNER JOIN texts
ON emails.email_id = texts.email_id
WHERE texts.action_date = emails.signup_date + INTERVAL '1 day'
  AND texts.signup_action = 'Confirmed';
```
#### Práctica 24 - Facebook/META SQL Interview Question Using Dates
```sql
SELECT user_id,
  EXTRACT(DAYS FROM (MAX(post_date) - MIN(post_date))) AS days_between
FROM posts
WHERE EXTRACT(YEAR FROM post_date) = '2021'
GROUP BY user_id
HAVING COUNT(post_id) > 1
ORDER BY user_id;
```
## Advanced SQL

### Lección 301
#### Práctica 1 - SQL Window Functions Practice Exercise
```sql
-- Añade tu solución aquí
```

#### Práctica 2 - SQL CTE (Common Table Expressions) Practice Exercise
```sql
-- Añade tu solución aquí
```

### Lección 302
#### Práctica 3 - SQL Recursive CTE Practice Exercise
```sql
-- Añade tu solución aquí
```

#### Práctica 4 - SQL Pivot Table Practice Exercise
```sql
-- Añade tu solución aquí
```

### Lección 303
#### Práctica 5 - SQL JSON Functions Practice Exercise
```sql
-- Añade tu solución aquí
```

#### Práctica 6 - SQL XML Functions Practice Exercise
```sql
-- Añade tu solución aquí
```

### Lección 304
#### Práctica 7 - SQL Full-Text Search Practice Exercise
```sql
-- Añade tu solución aquí
```

#### Práctica 8 - SQL Geospatial Functions Practice Exercise
```sql
-- Añade tu solución aquí
```
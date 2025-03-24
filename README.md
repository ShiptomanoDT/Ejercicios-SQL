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

### Lección 302
#### Práctica 1 - CTE & Subquery Example: Identify the Top-Selling Artist
```sql
WITH mayor_ingreso AS(
  SELECT 
    genre, MAX(concert_revenue/number_of_members) AS revenue_per_member
    FROM concerts
  GROUP BY genre
)

SELECT artist_name, concert_revenue, mi.genre, number_of_members,revenue_per_member
FROM mayor_ingreso AS mi
JOIN concerts AS c
ON mi.genre = c.genre
WHERE revenue_per_member * number_of_members = concert_revenue
ORDER BY revenue_per_member DESC,artist_name
```

#### Práctica 2 - Practice CTE and Subquery Interview Questions
```sql
SELECT c.customer_id 
FROM customer_contracts as c
LEFT JOIN products as p
ON c.product_id = p.product_id
GROUP BY c.customer_id
HAVING COUNT(DISTINCT(p.product_category))=
( 
  SELECT COUNT(DISTINCT(product_category))
  FROM products 
)  
```
#### Práctica 3 - Swapped Food Delivery
```sql
SELECT
  CASE
    WHEN order_id = (
      SELECT COUNT(order_id) 
      FROM orders
    ) THEN order_id
    ELSE order_id % 2 * 2 - 1 + order_id
  END AS ordenado_id, item
FROM orders
ORDER BY ordenado_id
```

### Lección 303
#### Práctica 4 - JP Morgan Aggregate Window Function SQL Interview Question
```sql
SELECT DISTINCT card_name,
  FIRST_VALUE(issued_amount) OVER (
    PARTITION BY (card_name) 
    ORDER BY issue_year, issue_month
  ) AS issued_amount
FROM monthly_cards_issued
ORDER BY issued_amount DESC;
```

### Lección 304
#### Práctica 5 - Top 5 Artists - Spotify SQL Interview Question
```sql
WITH ranking AS (
    SELECT artist_name, COUNT(rank),
    DENSE_RANK() OVER(ORDER BY COUNT(rank) DESC) AS artist_rank
    FROM artists AS a 
    JOIN songs AS s
    ON a.artist_id = s.artist_id 
    JOIN global_song_rank AS r
    ON s.song_id = r.song_id
    WHERE rank <= 10
    GROUP BY a.artist_name
)

SELECT artist_name, artist_rank
FROM ranking 
WHERE artist_rank <= 5
```

#### Práctica 6 - Walmart RANK SQL Interview Question
```sql
SELECT transaction_date, user_id, COUNT(product_id)
FROM user_transactions
WHERE (user_id,transaction_date) IN(
  SELECT user_id,MAX(transaction_date) 
  FROM user_transactions 
  GROUP BY user_id
)
GROUP BY user_id,transaction_date
ORDER BY transaction_date
```

#### Práctica 7 - Google RANK SQL Interview Question
```sql
SELECT DATE(measurement_time) AS measurement_day,
SUM(CASE 
      WHEN trans_rank %2 != 0 THEN measurement_value 
      ELSE 0 END
    ) AS odd_sum,
SUM(CASE 
      WHEN trans_rank %2 = 0 THEN measurement_value 
      ELSE 0 END
    ) AS even_sum
FROM (
  SELECT *, ROW_NUMBER() OVER (PARTITION BY DATE(measurement_time) 
    ORDER BY measurement_time) AS trans_rank
FROM measurements) AS temp_
GROUP BY measurement_day
ORDER BY measurement_day
```

### Lección 305
#### Práctica 8 - LEAD AND LAG Example: Analyzing Stocks Data
```sql
--No se logro
```

#### Práctica 9 - Y-on-Y Growth Rate - Wayfair SQL Interview Question
```sql
SELECT 
  EXTRACT(YEAR FROM transaction_date) AS year,
  product_id, spend AS curr_year_spend,
  LAG(spend) OVER(
    PARTITION BY product_id 
    ORDER BY transaction_date) AS prev_year_spend,
  ROUND(100 * (spend - LAG(spend) OVER(
    PARTITION BY product_id 
    ORDER BY transaction_date)) / LAG(spend) OVER(
    PARTITION BY product_id 
    ORDER BY transaction_date),2) AS yoy_rate
FROM user_transactions;
```

#### Práctica 10 - LEAD LAG SQL Interview Question
```sql
SELECT 
  EXTRACT(YEAR FROM transaction_date) AS year,
  product_id, spend AS curr_year_spend,
  LAG(spend) OVER(
    PARTITION BY product_id 
    ORDER BY transaction_date) AS prev_year_spend,
  ROUND(100 * (spend - LAG(spend) OVER(
    PARTITION BY product_id 
    ORDER BY transaction_date)) / LAG(spend) OVER(
    PARTITION BY product_id 
    ORDER BY transaction_date),2) AS yoy_rate
FROM user_transactions;
```

### Lección 307
#### Práctica 11 - Tricky UNION SQL Interview Question Asked By Amazon
```sql
--no se logro
```

#### Práctica 12 - Except Practice Exercise: FB SQL Interview Question
```sql
SELECT page_id 
FROM pages
WHERE page_id NOT IN (SELECT DISTINCT(page_id) FROM page_likes);
```

### Lección 311
#### Práctica 13 - SQL LOWER Practice Exercise 
```sql
SELECT *
FROM customers
WHERE LOWER(customer_name) LIKE '%son'AND gender = 'Male' AND age = 20;
```

#### Práctica 14 - CONCAT SQL Interview Question
```sql
SELECT manufacturer, CONCAT('$',ROUND( SUM(total_sales)*0.000001,0),' million') AS sale
FROM pharmacy_sales 
GROUP BY manufacturer
ORDER BY SUM(total_sales) DESC;
```
# Soluciones a las Prácticas de SQLZoo

## 0 SELECT basics
### 1. Introducing the world table of countries
- Modificando nombre de pais a:
```sql
SELECT population 
FROM world
WHERE name = 'Germany'
```
### 2. Scandinavia
- Modificando nombre de paises a:
```sql
SELECT name, population FROM world
  WHERE name IN ('Sweden', 'Norway', 'Denmark');
```
### 3. Just the right size
- Modificando nombre el intervalo de area a:
```sql
SELECT name, area
FROM world
WHERE area BETWEEN 200000 AND 250000
```
### QUIZ
Tabla de Pregunta
| name         | region       | area    | population | gdp          |
|--------------|--------------|---------|------------|--------------|
| Afghanistan  | South Asia   | 652225  | 26000000   |              |
| Albania      | Europe       | 28728   | 3200000    | 6656000000   |
| Algeria      | Middle East  | 2400000 | 32900000   | 75012000000  |
| Andorra      | Europe       | 468     | 64000      |              |
| ...          | ...          | ...     | ...        | ...          |

1. Select the code which produces this table 

| name         | population |
|--------------|------------|
| Bahrain      | 1234571    |
| Swaziland    | 1220000    |
| Timor-Leste  | 1066409    |

- Respuesta: 
```sql
SELECT name, population
  FROM world
 WHERE population BETWEEN 1000000 AND 1250000
```
2. Pick the result you would obtain from this code: 
```sql
SELECT name, population
      FROM world
      WHERE name LIKE "Al%"
```
- Respuesta: 

|          |            |
|----------|------------|
| Albania  | 3200000    |
| Algeria  | 32900000   |

3. Select the code which shows the countries that end in A or L 
- Respuesta: 
```sql
SELECT name FROM world
 WHERE name LIKE '%a' OR name LIKE '%l'
```
4. Pick the result from the query 
```sql
SELECT name,length(name)
FROM world
WHERE length(name)=5 and region='Europe'
```
- Respuesta: 

| name  | length(name) |
|-------|--------------|
| Italy | 5            |
| Malta | 5            |
| Spain | 5            |

5. Here are the first few rows of the world table: 

| name         | region       | area    | population | gdp          |
|--------------|--------------|---------|------------|--------------|
| Afghanistan  | South Asia   | 652225  | 26000000   |              |
| Albania      | Europe       | 28728   | 3200000    | 6656000000   |
| Algeria      | Middle East  | 2400000 | 32900000   | 75012000000  |
| Andorra      | Europe       | 468     | 64000      |              |
| ...          | ...          | ...     | ...        | ...          |

Pick the result you would obtain from this code: 
```sql
SELECT name, area*2 FROM world WHERE population = 64000
```
- Respuesta: 

|         |        |
|---------|--------|
| Andorra | 936    |

6. Select the code that would show the countries with an area larger than 50000 and a population smaller than 10000000 
- Respuesta: 
```sql
SELECT name, area, population
  FROM world
 WHERE area > 50000 AND population < 10000000
```
7. Select the code that shows the population density of China, Australia, Nigeria and France 
- Respuesta: 
```sql
SELECT name, population/area
  FROM world
 WHERE name IN ('China', 'Nigeria', 'France', 'Australia')
```

## 1 SELECT name
### Problemas
### 1. 
- Modificando LIKE a:
```sql
SELECT name FROM world
  WHERE name LIKE 'Y%'
```
### 2. 
- Modificando LIKE a:
```sql
SELECT name FROM world
  WHERE name LIKE '%y'
```
### 3. 
- Modificando LIKE a:
```sql
SELECT name FROM world
  WHERE name LIKE '%x%'
```
### 4. 
- Modificando LIKE a:
```sql
SELECT name FROM world
  WHERE name LIKE '%land'
```
### 5. 
- Modificando LIKE a:
```sql
SELECT name FROM world
  WHERE name LIKE 'C%ia'
```
### 6. 
- Modificando LIKE a:
```sql
SELECT name FROM world
  WHERE name LIKE '%oo%'
```
### 7. 
- Modificando LIKE a:
```sql
SELECT name FROM world
  WHERE name LIKE '%a%a%a%'
```
### 8. 
- Modificando LIKE a:
```sql
SELECT name FROM world
 WHERE name LIKE '_t%'
ORDER BY name
```
### 9. 
- Modificando LIKE a:
```sql
SELECT name FROM world
 WHERE name LIKE '%o__o%'
```
### 10. 
- Modificando agregando LENGHT:
```sql
SELECT name FROM world
 WHERE LENGTH(name) = 4
```
### 11. 
- Modificando consulta a:
```sql
SELECT name
  FROM world
 WHERE name = capital
```
### 12. 
- Modificando consulta a:
```sql
SELECT name
  FROM world
 WHERE capital = CONCAT(name,' City')
```
### 13. 
- Agregando consulta a:
```sql
SELECT capital, name
FROM world
WHERE capital LIKE CONCAT('%',name,'%')
```
### 14. 
- Agregando consulta a:
```sql
SELECT capital, name
FROM world
WHERE capital LIKE CONCAT('%',name,'%') 
AND LENGTH(capital)>LENGTH(name)
```
### 15. 
- Agregando consulta a:
```sql
SELECT name, REPLACE(capital,name,'')
FROM world
WHERE capital LIKE CONCAT('%',name,'%') 
AND LENGTH(capital)>LENGTH(name)
```
### QUIZ
Tabla de Pregunta
| name         | continent     | area    | population | gdp          |
|--------------|---------------|---------|------------|--------------|
| Afghanistan  | South Asia    | 652225  | 26000000   |              |
| Albania      | Europe        | 28728   | 3200000    | 6656000000   |
| Algeria      | Middle East   | 2400000 | 32900000   | 75012000000  |
| Andorra      | Europe        | 468     | 64000      |              |
| Brazil       | South America | 8550000 | 182800000  | 564852000000 |
| Colombia     | South America | 1140000 | 45600000   |              |
| Nauru        | Asia-Pacific  | 21      | 9900       |              |
| Uzbekistan   | Central Asia  | 447000  | 26000000   |              |

1. Select the code which gives the name of countries beginning with U 
- Respuesta: 
```sql
SELECT name
  FROM world
 WHERE name LIKE 'U%'
```
2. Select the code which shows just the population of United Kingdom? 
- Respuesta: 
```sql
SELECT population
  FROM world
 WHERE name = 'United Kingdom'
```
3. Select the answer which shows the problem with this SQL code - the intended result should be the continent of France:  
- Respuesta: 
_'name' should be name_
4. Select the result that would be obtained from the following code: 
- Respuesta: 

|Nauru | 990|
|------|----|

5. Select the code which would reveal the name and population of countries in Europe and Asia 
- Respuesta: 
```sql
SELECT name, population
  FROM world
 WHERE continent IN ('Europe', 'Asia')
```
6. Select the code which would give two rows 
- Respuesta: 
```sql
SELECT name FROM world
 WHERE name IN ('Cuba', 'Togo')
```
7. Select the result that would be obtained from this code: 
- Respuesta: 

|         |
|---------|
|Brazil   |
|Colombia |


## 2 SELECT from World
### Problemas
### 1. Introduction
- Observando:
```sql
SELECT name, continent, population FROM world
```
### 2. Large Countries
- Modificando condicion en WHERE a:
```sql
SELECT name FROM world
WHERE population >= 200000000
```
### 3. Per capita GDP
- Agregando consulta:
```sql
SELECT name, gdp/population AS GDP
FROM world
WHERE population > 200000000
```
### 4. South America In millions
- Agregando consulta:
```sql
SELECT name,population/1000000
FROM world
WHERE continent = 'South America'
```
### 5. France, Germany, Italy
- Agregando consulta:
```sql
SELECT name,population
FROM world
WHERE name IN('France','Germany','Italy')
```
### 6. United
- Agregando consulta:
```sql
SELECT name
FROM world
WHERE name LIKE '%United%'
```
### 7. Two ways to be big
- Agregando consulta:
```sql
SELECT name, population, area
FROM world
WHERE area > 3000000 OR population > 250000000
```
### 8. One or the other (but not both)
- Agregando consulta:
```sql
SELECT name, population, area
FROM world
WHERE area > 3000000 XOR population > 250000000
```
### 9. Rounding
- Agregando consulta:
```sql
SELECT name, ROUND(population/1000000,2) AS population, ROUND(GDP/1000000000,2) AS GDP
FROM world
WHERE continent = 'South America'
```
### 10. Trillion dollar economies
- Agregando consulta:
```sql
SELECT name, ROUND(gdp/population,-3) AS GDP
FROM world
WHERE gdp > 1000000000000 AND GDP
```
### 11. Name and capital have the same length
- Modificando a:
```sql
SELECT name, capital
FROM world
WHERE LENGTH(name)=LENGTH(capital)
```
### 12. Matching name and capital
- Modificando a:
```sql
SELECT name, capital
FROM world
WHERE LEFT(name,1)=LEFT(capital,1) AND name != capital
```
### 13. All the vowels
- Modificando a:
```sql
SELECT name
   FROM world
WHERE name LIKE '%a%' AND name LIKE '%e%' AND name LIKE '%i%' AND name LIKE '%o%' AND name LIKE '%u%' AND name NOT LIKE '% %'
```

## 3 SELECT from Nobel
### Problemas
### 1. Winners from 1950
- Modificando año:
```sql
SELECT yr, subject, winner
  FROM nobel
 WHERE yr = 1950
```
### 2. 1962 Literature
- Modificando año y materia:
```sql
SELECT winner
  FROM nobel
 WHERE yr = 1962
   AND subject = 'literature'
```
### 3. Albert Einstein
- Agregando consulta:
```sql
SELECT yr, subject
FROM nobel
WHERE winner = 'Albert Einstein'
```
### 4. Recent Peace Prizes
- Agregando consulta:
```sql
SELECT winner
FROM nobel
WHERE subject = 'peace' AND yr >= 2000
```
### 5. Literature in the 1980's
- Agregando consulta:
```sql
SELECT yr, subject, winner
FROM nobel
WHERE subject = 'literature' AND yr BETWEEN 1980 AND 1989
```
### 6. Only Presidents
- Modificando consulta:
```sql
SELECT * FROM nobel
 WHERE winner IN('Theodore Roosevelt', 'Thomas Woodrow Wilson', 'Jimmy Carter', 'Barack Obama')
```
### 7. John
- Agregando consulta:
```sql
SELECT winner
FROM nobel
WHERE winner LIKE 'John%'
```
### 8. Chemistry and Physics from different years
- Agregando consulta:
```sql
SELECT yr, subject, winner
FROM nobel
WHERE subject = 'physics' AND yr = 1980 OR subject = 'chemistry' AND yr = 1984
```
### 9. Exclude Chemists and Medics
- Agregando consulta:
```sql
SELECT yr, subject, winner
FROM nobel
WHERE yr = 1980 AND subject NOT IN('chemistry', 'medicine')
```
### 10. Early Medicine, Late Literature
- Agregando consulta:
```sql
SELECT yr, subject, winner
FROM nobel
WHERE subject = 'Medicine' AND yr < 1910 OR subject  = 'Literature' AND yr >= 2004
```
### Harder Questions - 11. Umlaut
- Agregando consulta a:
```sql
SELECT *
FROM nobel
WHERE winner LIKE 'PETER%BERG'
```
### Harder Questions - 12. Apostrophe
- Agregando consulta:
```sql
SELECT *
FROM nobel
WHERE winner LIKE 'EUGENE%NEILL'
```
### Harder Questions - 13. Knights of the realm
- Agregando consulta:
```sql
SELECT winner, yr, subject
FROM nobel
WHERE winner LIKE 'Sir%'
ORDER BY yr DESC, winner
```
### Harder Questions - 14. Chemistry and Physics last
- Modificando consulta:
```sql
SELECT winner, subject
FROM nobel
WHERE yr=1984
ORDER BY
 CASE
  WHEN subject IN ('physics','chemistry') THEN 1
  ELSE 0
 END,
 subject, winner
```

## 4 SELECT within SELECT
### Problemas
### 1. Bigger than Russia
- Modificando nombre de pais:
```sql
SELECT name FROM world
  WHERE population >
     (SELECT population FROM world
      WHERE name='Russia')
```
### 2. Richer than UK
- Agregando consulta:
```sql
SELECT name
FROM world
WHERE continent = 'Europe' AND gdp/population > (SELECT gdp/population FROM world WHERE name = 'United Kingdom') 
```
### 3. Neighbours of Argentina and Australia
- Agregando consulta:
```sql
SELECT name, continent
FROM world
WHERE continent IN (SELECT continent FROM world WHERE name = 'Argentina' OR name = 'Australia')
ORDER BY name
```
### 4. Between Canada and Poland
- Agregando consulta:
```sql
SELECT name, population
FROM world 
WHERE population > (SELECT population FROM world WHERE name = 'United Kingdom') AND population < (SELECT population FROM world WHERE name = 'Germany')
```
### 5. Percentages of Germany
- Agregando consulta:
```sql
SELECT name, CONCAT(ROUND((population*100)/(SELECT population FROM world WHERE name='Germany')),'%')AS Percentage
FROM world
WHERE continent = 'Europe'
ORDER BY name
```
### 6. Bigger than every country in Europe
- Modificando consulta:
```sql
SELECT name
  FROM world
 WHERE gdp >= (SELECT MAX(gdp)
                          FROM world
                          WHERE gdp>0 AND continent = 'Europe') AND continent != 'Europe'
```
### 7. Largest in each continent
- Modificando consulta a:
```sql
SELECT continent, name, area FROM world x
  WHERE area >=
(SELECT MAX(area) FROM world y
        WHERE y.continent=x.continent
          AND population>0)  
```
### 8. First country of each continent (alphabetically)
- Agregando consulta:
```sql
SELECT continent, name
FROM world
GROUP BY continent
```
### 9. Difficult Questions That Utilize Techniques Not Covered In Prior Sections
- Agregando consulta:
```sql
SELECT name, continent, population
FROM world
WHERE continent IN(SELECT continent 
                   FROM world 
                   GROUP BY continent
                   HAVING MAX(population) <=25000000
)
```
### 10. Three time bigger
- Agregando consulta:
```sql
SELECT w1.name, w1.continent
FROM world w1
WHERE NOT EXISTS(
    SELECT *
    FROM world w2
    WHERE w2.continent = w1.continent
      AND w2.name != w1.name
      AND w1.population <=3 * w2.population
);
```

## 5 SUM and COUNT
### Problemas
### 1. Total world population
- Observando:
```sql
SELECT SUM(population)
FROM world
```
### 2. List of continents
- Agregando consulta:
```sql
SELECT DISTINCT continent
FROM world
```
### 3. GDP of Africa
- Agregando consulta:
```sql
SELECT SUM(gdp)
FROM world
WHERE continent = 'Africa'
```
### 4. Count the big countries
- Agregando consulta:
```sql
SELECT COUNT(*) AS Countrys
FROM world
WHERE area > 1000000
```
### 5. Baltic states population
- Agregando consulta:
```sql
SELECT SUM(population)
FROM world
WHERE name IN('Estonia', 'Latvia', 'Lithuania')
```
### 6. Using GROUP BY and HAVING - Counting the countries of each continent
- Agregando consulta:
```sql
SELECT continent, COUNT(name)
FROM world
GROUP BY continent
```
### 7. Counting big countries in each continent
- Agregando consulta:
```sql
SELECT continent, COUNT(name)
FROM world
WHERE population >= 10000000
GROUP BY continent
```
### 8. Counting big continents
- Agregando consulta:
```sql
SELECT continent
FROM world
GROUP BY continent
HAVING SUM(population)>=100000000
```

## 6 JOIN
### Problemas
### 1. 
- Modificando a:
```sql
SELECT matchid,player
FROM goal 
WHERE teamid = 'GER'
```
### 2.
- Agregando condicion con WHERE:
```sql
SELECT id,stadium,team1,team2
  FROM game
WHERE id = 1012
```
### 3. 
- Modificando consulta a:
```sql
SELECT player, teamid, stadium, mdate
  FROM game JOIN goal ON (id=matchid)
WHERE teamid = 'GER'
```
### 4. 
- Agregando consulta:
```sql
SELECT team1, team2, player
  FROM game JOIN goal ON (id=matchid)
WHERE player LIKE 'Mario%'
```
### 5. 
- Modificando consulta a:
```sql
SELECT player, teamid, coach, gtime
  FROM  goal JOIN eteam ON teamid=id
 WHERE gtime<=10
```
### 6. 
- Agregando consulta:
```sql
SELECT mdate, teamname
FROM game g JOIN eteam e
  ON g.team1 = e.id
WHERE coach = 'Fernando Santos'
```
### 7. 
- Agregando consulta:
```sql
SELECT player
FROM game g JOIN goal go
  ON g.id = go.matchid
WHERE stadium = 'National Stadium, Warsaw'
```
### 8. More difficult questions
- Modificando consulta a:
```sql
SELECT DISTINCT player
  FROM game JOIN goal ON matchid = id 
    WHERE (team1='GER' OR team2='GER') AND teamid != 'GER'
```
### 9. 
- Modificando consulta a:
```sql
SELECT teamname, COUNT(matchid) AS total_goals
  FROM eteam JOIN goal ON id=teamid
 GROUP BY teamname
```
### 10. 
- Agregando consulta:
```sql
SELECT stadium, COUNT(matchid) AS total_goals
  FROM game JOIN goal ON id=matchid
 GROUP BY stadium
```
### 11. 
- Modificando consulta a:
```sql
SELECT matchid, mdate, COUNT(teamid)
  FROM game JOIN goal ON matchid = id 
 WHERE (team1 = 'POL' OR team2 = 'POL')
GROUP BY matchid
```
### 12. 
- Agregando consulta:
```sql
SELECT matchid, mdate, COUNT(teamid)
  FROM game JOIN goal ON matchid = id 
 WHERE (team1 = 'GER' OR team2 = 'GER') AND teamid = 'GER'
GROUP BY matchid
```
### 13. 
- Modificando consulta a:
```sql
SELECT mdate,
  team1,
  SUM(CASE WHEN teamid=team1 THEN 1 ELSE 0 END) score1,
  team2,
  SUM(CASE WHEN teamid=team2 THEN 1 ELSE 0 END) score2
  FROM game LEFT JOIN goal ON matchid = id
GROUP BY mdate,team1
ORDER BY mdate,matchid,team1,team2
```

## 7 More JOIN operations
### Problemas
### 1. 1962 movies
- Observando:
```sql
SELECT id, title
 FROM movie
 WHERE yr=1962
```
### 2. When was Citizen Kane released?
- Agregando consulta:
```sql
SELECT yr
FROM movie
WHERE title = 'Citizen Kane'
```
### 3. Star Trek movies
- Agregando consulta:
```sql
SELECT id, title, yr
FROM movie
WHERE title LIKE '%Star Trek%'
ORDER BY yr
```
### 4. id for actor Glenn Close 
- Agregando consulta:
```sql
SELECT id
FROM actor
WHERE name = 'Glenn Close'
```
### 5. id for Casablanca
- Agregando consulta:
```sql
SELECT id
FROM movie
WHERE title = 'Casablanca'
```
### 6. Cast list for Casablanca
- Agregando consulta:
```sql
SELECT name
FROM actor JOIN casting
ON id = actorid
WHERE movieid = 11768
```
### 7. Alien cast list
- Agregando consulta:
```sql
SELECT name
FROM actor JOIN casting
ON id = actorid
WHERE movieid = (SELECT id FROM movie WHERE title = 'Alien')
```
### 8. Harrison Ford movies
- Agregando consulta:
```sql
SELECT title
FROM movie JOIN casting
ON id = movieid
WHERE actorid = (SELECT id FROM actor WHERE name = 'Harrison Ford')
```
### 9. Harrison Ford as a supporting actor
- Agregando consulta:
```sql
SELECT title
FROM movie JOIN casting
ON id = movieid
WHERE actorid = (SELECT id FROM actor WHERE name = 'Harrison Ford') AND ord != 1
```
### 10. Lead actors in 1962 movies
- Agregando consulta:
```sql
SELECT title, name
FROM movie JOIN (SELECT name, movieid
                 FROM actor JOIN casting 
                 ON id = actorid
                 WHERE ord = 1) AS acas
ON id = movieid
WHERE yr = 1962
```
### 11. Busy years for Rock Hudson
- Modificando consulta a:
```sql
SELECT yr,COUNT(title) FROM
  movie JOIN casting ON movie.id=movieid
        JOIN actor   ON actorid=actor.id
WHERE name='Rock Hudson'
GROUP BY yr
HAVING COUNT(title) > 2
```
### 12. 
- Modificando consulta a:
```sql
SELECT DISTINCT title, name
FROM actor
JOIN casting ON id = actorid
JOIN (SELECT title, movieid 
      FROM casting 
      JOIN movie ON movieid = id
      WHERE actorid IN (
      SELECT id FROM actor
      WHERE name='Julie Andrews')) AS moviecast
ON casting.movieid = moviecast.movieid
WHERE casting.ord = 1
```
### 13. Actors with 15 leading roles
- Agregando consulta:
```sql
SELECT name
FROM actor 
JOIN casting ON id = actorid
WHERE ord = 1 
GROUP BY name
HAVING COUNT(movieid)>=15
ORDER BY name
```
### 14. released in the year 1978
- Agregando consulta:
```sql
SELECT title, COUNT(actorid)
FROM movie
JOIN casting ON id = movieid
WHERE yr = 1978
GROUP BY title
ORDER BY COUNT(actorid) DESC, title
```
### 15. with 'Art Garfunkel'
- Agregando consulta:
```sql
SELECT name
FROM actor
JOIN casting ON id = actorid
WHERE movieid IN(SELECT movieid 
                FROM casting 
                JOIN movie ON movieid = id
                WHERE actorid IN (SELECT id FROM actor
                                  WHERE name='Art Garfunkel')
                )
AND name != 'Art Garfunkel'
```

## 8 Using Null
### Problemas
### 1. NULL, INNER JOIN, LEFT JOIN, RIGHT JOIN
- Agregando consulta:
```sql
SELECT name
FROM teacher
WHERE dept IS NUL
```
### 2.
- Observando:
```sql
SELECT teacher.name, dept.name
 FROM teacher INNER JOIN dept
           ON (teacher.dept=dept.id)
```
### 3. 
- Agregando consulta:
```sql
SELECT t.name, d.name
FROM teacher t
LEFT JOIN dept d
  ON t.dept = d.id
```
### 4.
- Agregando consulta:
```sql
SELECT t.name, d.name 
FROM teacher t
RIGHT JOIN dept d
  ON t.dept = d.id
```
### 5. 
- Agregando consulta:
```sql
SELECT name, COALESCE(mobile,'07986 444 2266')
FROM teacher
```
### 6.
- Agregando consulta:
```sql
SELECT t.name, COALESCE(d.name, 'None')
FROM teacher t
LEFT JOIN dept d
  ON t.dept = d.id
```
### 7. 
- Agregando consulta:
```sql
SELECT COUNT(name), COUNT(mobile)
FROM teacher
```
### 8.
- Agregando consulta:
```sql
SELECT  d.name, COUNT(t.name)
FROM teacher t RIGHT JOIN dept d
  ON t.dept = d.id
GROUP BY d.name
```
### 9. 
- Agregando consulta:
```sql
SELECT t.name, CASE 
         WHEN t.dept = 1 OR t.dept = 2 THEN 'Sci'
         ELSE 'Art'
       END
FROM teacher t LEFT JOIN dept d
  ON t.dept = d.id

```
### 10. 
- Agregando consulta:
```sql
SELECT t.name, CASE 
         WHEN t.dept IN(1,2) THEN 'Sci'
         WHEN t.dept = 3 THEN 'Art'
         ELSE 'None'
       END
FROM teacher t LEFT JOIN dept d
  ON t.dept = d.id
```

## 8+ Numeric Examples
### Problemas
### 1. Check out one row
- Modificando consulta a:
```sql
SELECT A_STRONGLY_AGREE
  FROM nss
 WHERE question='Q01'
   AND institution='Edinburgh Napier University'
   AND subject='(8) Computer Science'
```
### 2. Calculate how many agree or strongly agree
- Modificando consulta a:
```sql
SELECT institution, subject
  FROM nss
 WHERE question='Q15' AND score >= 100
```
### 3. Unhappy Computer Students
- Modificando consulta a:
```sql
SELECT institution, score
  FROM nss
 WHERE question='Q15'
   AND score < 50
   AND subject='(8) Computer Science'
```
### 4. More Computing or Creative Students?
- Modificando consulta a:
```sql
SELECT subject, SUM(response)
  FROM nss
 WHERE question='Q22'
   AND subject IN('(8) Computer Science', '(H) Creative Arts and Design')
GROUP BY subject
```
### 5. Strongly Agree Numbers
- Modificando consulta a:
```sql
SELECT subject, SUM(response*A_STRONGLY_AGREE/100)
  FROM nss
 WHERE question='Q22'
   AND subject IN('(8) Computer Science', '(H) Creative Arts and Design')
GROUP BY subject
```
### 6. Strongly Agree, Percentage
- Agregando consulta:
```sql
SELECT subject, ROUND(SUM(response*A_STRONGLY_AGREE)/SUM(response))
  FROM nss
 WHERE question='Q22'
   AND subject IN('(8) Computer Science', '(H) Creative Arts and Design')
GROUP BY subject
```
### 7. Scores for Institutions in Manchester
- Modificando consulta a:
```sql
SELECT institution, ROUND(SUM(score*response)/SUM(response)) AS score
  FROM nss
 WHERE question='Q22'
   AND institution LIKE '%Manchester%'
GROUP BY institution
```
### 8. Number of Computing Students in Manchester
- Modificando consulta a:
```sql
SELECT 
    institution, 
    SUM(sample) AS total_sample,
    SUM(CASE 
          WHEN subject LIKE '%Computer Science%' THEN sample 
          ELSE 0 
        END) AS comp
FROM nss
WHERE question = 'Q01'
  AND institution LIKE '%Manchester%'
GROUP BY institution;
```
## 9- Window function
### Problemas
### 1. Warming up
- Modificando consulta a:
```sql
SELECT lastName, party, votes
  FROM ge
 WHERE constituency = 'S14000024' AND yr = 2017 /*se cambio constituency*/
ORDER BY votes DESC
```
### 2. Who won?
- Modificando consulta a:
```sql
SELECT party, votes, 
       RANK() OVER (ORDER BY votes DESC) as posn
  FROM ge
 WHERE constituency = 'S14000024' AND yr = 2017
ORDER BY party
```
### 3. PARTITION BY
- Observando:
```sql
SELECT yr,party, votes,
      RANK() OVER (PARTITION BY yr ORDER BY votes DESC) as posn
  FROM ge
 WHERE constituency = 'S14000021'
ORDER BY party,yr
```
### 4. Edinburgh Constituency
- Modificando consulta a:
```sql
SELECT constituency,party, votes, 
       RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS posn
  FROM ge
 WHERE constituency BETWEEN 'S14000021' AND 'S14000026'
   AND yr  = 2017
ORDER BY posn, constituency
```
### 5. Winners Only
- Modificando consulta a:
```sql
SELECT ge.constituency, ge.party
  FROM ge JOIN (SELECT constituency,party, votes, 
       RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS posn
                FROM ge
                WHERE constituency BETWEEN 'S14000021' AND 'S14000026'
                AND yr  = 2017
                ORDER BY posn, constituency
               ) ge2
  ON ge.party = ge2.party AND ge.constituency =ge2.constituency
WHERE ge2.posn = 1
GROUP BY constituency
```
### 6. Scottish seats
- Modificando consulta a:
```sql
SELECT ge.party, COUNT(1)
  FROM ge JOIN (SELECT constituency, party, votes,
       RANK() OVER (PARTITION BY constituency ORDER BY votes DESC) AS posn
                FROM ge
                WHERE constituency LIKE 'S%'
                AND yr  = 2017
               ) ge2
  ON ge.party = ge2.party AND ge.constituency = ge2.constituency AND ge.votes = ge2.votes
WHERE ge2.posn = 1
GROUP BY ge.party
```

## 9+ COVID 19
### Problemas
### 1. Introducing the covid table
- Modificando nombre de pais a:
```sql
SELECT name, DAY(whn),
 confirmed, deaths, recovered
 FROM covid
WHERE name = 'Spain'
AND MONTH(whn) = 3 AND YEAR(whn) = 2020
ORDER BY whn
```
### 2. Introducing the LAG function
- Modificando consulta a:
```sql
SELECT name, DAY(whn), confirmed,
   LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn)
 FROM covid
WHERE name = 'Italy'
AND MONTH(whn) = 3 AND YEAR(whn) = 2020
ORDER BY whn
```
### 3. Number of new cases
- Modificando consulta a:
```sql
SELECT name, DAY(whn),
   confirmed - LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) AS new
 FROM covid
WHERE name = 'Italy'
AND MONTH(whn) = 3 AND YEAR(whn) = 2020
ORDER BY whn
```
### 4. Weekly changes
- Modificando consulta a:
```sql
SELECT name, DATE_FORMAT(whn,'%Y-%m-%d'), confirmed - LAG(confirmed, 1) OVER (PARTITION BY name ORDER BY whn) AS new
 FROM covid
WHERE name = 'Italy'
AND WEEKDAY(whn) = 0 AND YEAR(whn) = 2020
ORDER BY whn
```
### 5. LAG using a JOIN
- Modificando consulta a:
```sql
SELECT tw.name, DATE_FORMAT(tw.whn,'%Y-%m-%d'), 
 tw.confirmed - lw.confirmed
 FROM covid tw LEFT JOIN covid lw ON 
  DATE_ADD(lw.whn, INTERVAL 1 WEEK) = tw.whn
   AND tw.name=lw.name
WHERE tw.name = 'Italy'
AND WEEKDAY(tw.whn) = 0
ORDER BY tw.whn
```
### 6. RANK()
- Modificando consulta a:
```sql
SELECT 
   name,
   confirmed,
   RANK() OVER (ORDER BY confirmed DESC) rc,
   deaths,
   RANK() OVER (ORDER BY deaths DESC) rc
  FROM covid
WHERE whn = '2020-04-20'
ORDER BY confirmed DESC
```
### 7. Infection rate
- Modificando consulta a:
```sql
SELECT 
   world.name,
   ROUND(100000 * confirmed / population, 2),
   RANK() OVER (ORDER BY (100000 * confirmed / population)) AS rank
FROM covid 
JOIN world ON covid.name = world.name
WHERE whn = '2020-04-20' 
  AND population > 10000000
ORDER BY population DESC;
```
### 8. Turning the corner
- Modificando consulta a:
```sql
/*No se pudo solucionar*/
```

## 9 Self join
### Problemas
### 1. 
- Agregando consulta:
```sql
SELECT COUNT(id)
FROM stops
```
### 2. 
- Agregando consulta:
```sql
SELECT id
FROM stops
WHERE name = 'Craiglockhart' 
```
### 3. 
- Agregando consulta:
```sql
SELECT id, name
FROM stops JOIN route ON id = stop
WHERE num = 4 AND company = 'LRT'
ORDER BY pos
```
### 4. Routes and stops
- Modificando consulta a:
```sql
SELECT company, num, COUNT(*)
FROM route WHERE stop=149 OR stop=53
GROUP BY company, num
HAVING COUNT(*) = 2
```
### 5. 
- Modificando consulta a:
```sql
SELECT a.company, a.num, a.stop, b.stop
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
WHERE a.stop=53 AND b.stop = 149
```
### 6. 
- Modificando consulta a:
```sql
SELECT a.company, a.num, stopa.name, stopb.name
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name='London Road'
```
### 7. Using a self join
- Agregando consulta:
```sql
SELECT DISTINCT a.company, a.num
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
WHERE a.stop=115 AND b.stop = 137
```
### 8. 
- Agregando consulta:
```sql
SELECT a.company, a.num
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND stopb.name='Tollcross'
```
### 9. 
- Agregando consulta:
```sql
SELECT stopb.name, a.company, a.num
FROM route a JOIN route b ON
  (a.company=b.company AND a.num=b.num)
  JOIN stops stopa ON (a.stop=stopa.id)
  JOIN stops stopb ON (b.stop=stopb.id)
WHERE stopa.name='Craiglockhart' AND a.company = 'LRT'
```
### 10. 
- Agregando consulta, la solucion se considera erronea por no tener el mismo orden, pero las tablas son las mismas:
```sql
SELECT DISTINCT
  r1.num,
  r1.company,
  t.name,
  r2.num,
  r2.company
FROM route r1
  JOIN stops s1 ON r1.stop = s1.id
  JOIN route r1t ON (r1.company = r1t.company AND r1.num = r1t.num)
  JOIN stops t ON r1t.stop = t.id
  JOIN route r2 ON t.id = r2.stop
  JOIN route r2l ON (r2.company = r2l.company AND r2.num = r2l.num)
  JOIN stops s2 ON r2l.stop = s2.id
WHERE s1.name = 'Craiglockhart'
  AND s2.name = 'Lochend';
```

# Soluciones a las Prácticas de Beecrowd

## Nivel 1

### 1. Customer Address
```sql
-- Añade tu solución aquí
```

### 2. Providers' City in Alphabetical Order
```sql
-- Añade tu solución aquí
```

### 3. Higher and Lower Price
```sql
-- Añade tu solución aquí
```

### 4. Expanding the Business
```sql
-- Añade tu solución aquí
```

### 5. Provider Ajax SA
```sql
-- Añade tu solución aquí
```

### 6. Legal Person
```sql
-- Añade tu solución aquí
```

### 7. Passwords
```sql
-- Añade tu solución aquí
```

### 8. Viruses
```sql
-- Añade tu solución aquí
```

## Nivel 2

### 9. Under 10 or Greater Than 100
```sql
-- Añade tu solución aquí
```

### 10. Cheap Movies
```sql
-- Añade tu solución aquí
```

### 11. Super Luxury
```sql
-- Añade tu solución aquí
```

### 12. How much earn a Doctor?
```sql
-- Añade tu solución aquí
```

### 13. Sillas Adyacentes
```sql
-- Añade tu solución aquí
```

### 14. Clasificación de un Árbol
```sql
-- Añade tu solución aquí
```

### 15. Seguidores
```sql
-- Añade tu solución aquí
```

### 16. Segundo Mayor y Menor
```sql
-- Añade tu solución aquí
```

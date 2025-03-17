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
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

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
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

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
### QUIZ
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

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
### QUIZ
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

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
### QUIZ
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

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
### QUIZ
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

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
### QUIZ
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

## 7 More JOIN operations
### Problemas
1. 
```sql
-- Añade tu solución aquí
```
2. 
```sql
-- Añade tu solución aquí
```
### QUIZ
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

## 8 Using Null
### Problemas
1. 
```sql
-- Añade tu solución aquí
```
2. 
```sql
-- Añade tu solución aquí
```
### QUIZ
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

## 8+ Numeric Examples
### Problemas
1. 
```sql
-- Añade tu solución aquí
```
2. 
```sql
-- Añade tu solución aquí
```
### QUIZ
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

## 9- Window function
### Problemas
1. 
```sql
-- Añade tu solución aquí
```
2. 
```sql
-- Añade tu solución aquí
```
### QUIZ
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

## 9+ COVID 19
### Problemas
1. 
```sql
-- Añade tu solución aquí
```
2. 
```sql
-- Añade tu solución aquí
```
### QUIZ
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

## 9 Self join
### Problemas
1. 
```sql
-- Añade tu solución aquí
```
2. 
```sql
-- Añade tu solución aquí
```
### QUIZ
| Pregunta | Respuesta |
|----------|-----------|
| Pregunta 1 | ![Respuesta 1](ruta/a/imagen1.png) |
| Pregunta 2 | ![Respuesta 2](ruta/a/imagen2.png) |

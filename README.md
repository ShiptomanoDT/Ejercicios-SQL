# Ejercicios-SQL
Ejercicios de Laboratorio
# Soluciones a las Prácticas de DataLemur

## Basic SQL

### Lección 101
#### Práctica 1 - SQL Select Practice Exercise
```python
SELECT product_id, product_category, product_name FROM products
```
#### Práctica 2 - WHERE Practice Exercise
```python
SELECT user_id,stars 
FROM reviews
WHERE stars=3;
```
#### Práctica 3 - SQL WHERE AND Practice Exercise
```python
SELECT *
FROM reviews
WHERE stars > 3 
  AND review_id < 6000
  AND review_id >2000
  AND user_id != 142;
```
#### Práctica 4 - SQL AND OR Practice Exercise
```python
SELECT * 
FROM reviews
WHERE (stars > 2 AND stars <= 4) 
  AND (user_id = 123
  OR user_id = 265
  OR user_id = 362);
```
#### Práctica 5 - SQL BETWEEN Practice Exercise
```python
SELECT manufacturer, drug, units_sold 
FROM pharmacy_sales
WHERE (manufacturer = 'AbbVie'
  OR manufacturer = 'Biogen'
  OR manufacturer = 'Eli Lilly')
  AND units_sold BETWEEN 100000 AND 105000;
```
#### Práctica 6 - SQL IN Practice Exercise
```python
SELECT manufacturer, drug, units_sold
FROM pharmacy_sales
WHERE manufacturer IN('Roche','Bayer','AstraZeneca') 
 AND units_sold NOT BETWEEN 55000 AND 550000;
```

### Lección 102
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 102
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 102
```

### Lección 103
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 103
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 103
```

### Lección 104
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 104
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 104
```

### Lección 105
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 105
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 105
```

### Lección 106
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 106
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 106
```

### Lección 107
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 107
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 107
```

### Lección 108
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 108
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 108
```

### Lección 109
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 109
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 109
```

## Intermediate SQL

### Lección 201
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 201
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 201
```

### Lección 202
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 202
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 202
```

### Lección 203
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 203
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 203
```

### Lección 204
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 204
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 204
```

### Lección 205
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 205
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 205
```

### Lección 206
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 206
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 206
```

### Lección 207
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 207
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 207
```

### Lección 208
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 208
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 208
```

### Lección 209
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 209
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 209
```

### Lección 210
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 210
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 210
```

### Lección 211
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 211
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 211
```

### Lección 212
#### Práctica 1
```python
# Código de la solución para la práctica 1 de la lección 212
```
#### Práctica 2
```python
# Código de la solución para la práctica 2 de la lección 212
```
```

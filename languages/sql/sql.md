## Basics

## Core Operations (CRUD)
> 1\. `CREATE` &rarr; insert new data <br>
> 2\. `READ` &rarr; get data <br>
> 3\. `UPDATE` &rarr; modify data <br>
> 4\. `DELETE` &rarr; remove data

```js
// create table
CREATE TABLE users (
  id INT PRIMARY KEY,
  name VARCHAR(100),
  age INT
);

// insert data
INSERT INTO users (id, name, age)
VALUES (1, 'Hussain', 22);

// insert multiple data values into table
INSERT INTO users VALUES
(2, 'A', 20),
(3, 'B', 21);

// read data
SELECT * FROM users;
// specific columns
SELECT name, age FROM users;
// with condition
SELECT * FROM users
WHERE age > 21;

// update data
UPDATE users
SET age = 23
WHERE id = 1;

// delete data
DELETE FROM users
WHERE id = 1;
```
## Other
```js
// delete table
DROP TABLE users;

// clear table
TRUNCATE TABLE users;
```

## Filters, Sorts, Limit, Aggregates, Groups
```js
// filters
WHERE age = 20
WHERE age != 20
WHERE age > 18
WHERE age BETWEEN 18 AND 25
WHERE name LIKE 'Hu%'

// sorts
SELECT * FROM users
ORDER BY age ASC;

SELECT * FROM users
ORDER BY age DESC;

// limit
SELECT * FROM users
LIMIT 5;

// aggregates
SELECT COUNT(*) FROM users;
SELECT AVG(age) FROM users;
SELECT MAX(age) FROM users;
SELECT MIN(age) FROM users;
SELECT SUM(age) FROM users;

// grouping
SELECT age, COUNT(*)
FROM users
GROUP BY age;
```

## Keys
`PRIMARY KEY` &rarr; unique row identifier

`FOREIGN KEY` &rarr; referencess another table

`UNIQUE` &rarr; no duplicats

`NOT NULL` &rarr; required field

## Joins
```js
// inner join
SELECT *
FROM users
JOIN orders
ON users.id = orders.user_id;

// left join
SELECT *
FROM users
LEFT JOIN orders
ON users.id = orders.user_id;
```

## Datatypes (in PostgreSQL)
```txt
INTEGER
BIGINT
SERIAL      - auto increment int
BIGSERIAL   - auto increment big int
VARCHAR(n)
TEXT
BOOLEAN
DATE
TIMESTAMP
JSON/JSONB
```
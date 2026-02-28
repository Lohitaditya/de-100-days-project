# SQL – Day 2

- SQL Command types (DDL, DML, DQL, TCL)

DDL: data definition language
CREATE, ALTER, DROP
DDL changes the shape of database.

DML: Data manipulation language
UPDATE, INSERT, DELETE
DML changes content of the table.

DQL: data query Language
SELECT
DQL only reads and retrievs, no changes.

TCL: transaction control language
COMMIT, ROLLBACK
TCL decides whether changes stay or go.

- Basic queries: SELECT, FROM, WHERE

SELECT + FROM:

SELECT COLUMN1, COLUMN2
FROM TABLE_NAME;

SELECT NAME,EMAIL
FROM USERS;

WHERE:

SELECT EMPLOYEE_ID
FROM EMP_TABLE
WHERE EMPLOYEE_SALARY < 5000;

SELECT *
FROM users
WHERE country = 'India';

Common where operators:
<, >, =, AND, OR

- Data types & constraints

Datatypes:

Numeric: INT, DECIMAL
String: VARCHAR, TEXT
Date/Time: DATE, TIMESTAMP

CREATE TABLE orders(
    order_id INT,
    order_amount DECIMAL(10,2),
    order_date DATE
)

Constraints:

primary key, foreign key, unique, not null

primary key: id of primary table, no duplicates, cant be null
foreign key: relates to another table's primary key
unique: enforces a column to have unique values in table
not null: value must exist even if it is 0

- Practice queries

Assume this table:

users
------------------------
user_id | name | age | country

*QUERY 1:
SELECT NAME, COUNTRY
FROM USERS;

*QUERY 2:
SELECT *
FROM USERS
WHERE AGE > 30;

*QUERY 3:
SELECT *
FROM USERS
WHERE country = 'India' AND age > 25;

*QUERY 4:
CREATE TABLE EMPLOYEES(
    emp_id INT PRIMARY KEY,
    name VARCHAR(50) NOT NULL,
    email VARCHAR(50) UNIQUE
);

## WHAT I CONFUSED ABOUT:

- WHEN TO USE DECIMAL VS FLOAT VS DOUBLE
DECIMAL(p,s) : Money, exact values
FLOAT : Approximate values
DOUBLE : Approximate values, higher precision

- HOW FOREIGN KEY SYNTAX WORKS EXACTLY

CREATE TABLE orders(
    order_id INT PRIMARY KEY,
    user_id INT,
    FOREIGN KEY (user_id) REFERENCES users(user_id)
);

- Foreign key references primary key of another table
- Enforces data integrity


# SQL - Day 3

## Filtering Operators

- AND → all conditions must be true
- OR → any condition can be true
- NOT → excludes rows
- IN → cleaner alternative to multiple OR conditions
- BETWEEN → filters a range (inclusive)
- LIKE → pattern matching for strings

Example:
```sql
SELECT *
FROM users
WHERE country IN ('India', 'USA')
  AND age BETWEEN 20 AND 35;

ORDER BY

Used to sort query results.
ASC → ascending order (default)
DESC → descending order

Example:
SELECT *
FROM users
ORDER BY age DESC;

GROUP BY

Used to aggregate data into groups.

Common aggregate functions:
COUNT()
SUM()
AVG()

Example:
SELECT user_id, COUNT(*) AS total_orders
FROM orders
GROUP BY user_id;

Rule:

All selected columns must be either:
part of GROUP BY, or
aggregate functions

HAVING

Used to filter aggregated results.

Example:
SELECT user_id, COUNT(*) AS total_orders
FROM orders
GROUP BY user_id
HAVING COUNT(*) > 2;

WHERE vs HAVING

WHERE → filters rows before grouping
HAVING → filters groups after aggregation

Execution order:
FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY


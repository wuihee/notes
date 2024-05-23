# SQL

- **Definition**: SQL is a *declarative* language, meaning you describe the data you want without specifying how to retrieve it.

## Relational Databases

- **Definition**: Relational databases store data in tables and *relate* data between tables through foreign keys.
- **Structure**:
  - **Tables**: Comparable to an Excel sheet.
  - **Rows (Tuples / Records)**: Each row represents a single record.
  - **Columns (Attributes)**: Each column represents a data field within the record.
  - **Entries**: All the information in one row constitutes an entry.

## Data Definition Language (DDL)

- `CREATE TABLE`: Creates a new table.

```sql
CREATE TABLE table_name (
    column1 datatype PRIMARY KEY,
    column2 datatype,
    ...
);
```

- `DROP TABLE`: Deletes a table.

```sql
DROP TABLE table_name
```

## Data Manipulation Language (DML)

- `SELECT`: Retrieves data from a database.

```sql
SELECT column1, column2, ...
FROM table_name
WHERE condition;

-- Using DISTINCT to avoid duplicate results
SELECT DISTINCT column1
FROM table_name;

-- Using WHERE to filter results
SELECT column1, column2
FROM table_name
WHERE condition;

-- Using AND/OR to combine conditions
SELECT column1, column2
FROM table_name
WHERE condition1 AND condition2;

SELECT column1, column2
FROM table_name
WHERE condition1 OR condition2;

-- Using LIKE for pattern matching
SELECT column1, column2
FROM table_name
WHERE column1 LIKE 'pattern%';

-- Sorting results with ORDER BY
SELECT column1, column2
FROM table_name
ORDER BY column1 ASC;  -- ASC for ascending order

SELECT column1, column2
FROM table_name
ORDER BY column1 DESC;  -- DESC for descending order

-- Limiting the number of results with LIMIT
SELECT column1, column2
FROM table_name
LIMIT number;
```

- `INSERT`: Insert a record into an existing table.

```sql
INSERT INTO table_name column1, column2, column3, ...
VALUES value1, value2, value3, ...;

-- Using RETURNING to get the inserted record
INSERT INTO table_name (column1, column2, column3, ...)
VALUES (value1, value2, value3, ...)
RETURNING column1, column2, column3;
```

- `UPDATE`: Modifies existing records in a table.

```sql
UPDATE table_name
SET column1 = value1, column2 = value2, ...
WHERE condition;
```

- `DELETE`: Delete an existing record in the table.

```sql
DELETE FROM table_name
WHERE condition;
```

## SQL Functions

```sql
SELECT AVG(column_name)
FROM table_name;

SELECT ROUND(column_name)
FROM table_name;
```

## Subqueries

- **Definition**: A subquery is a query within another query. The subquery is executed first, and its result is used by the outer query.

```sql
-- Subquery in WHERE clause
SELECT column1, column2
FROM table_name
WHERE column1 IN (SELECT column1 FROM another_table WHERE condition);

-- Subquery in FROM clause
SELECT subquery.column1, subquery.column2
FROM (SELECT column1, column2 FROM table_name WHERE condition) AS subquery;

-- Subquery in SELECT clause
SELECT column1,
    (SELECT COUNT(*) FROM another_table WHERE another_table.foreign_key = table_name.primary_key) AS count_alias
FROM table_name;
```

## JOIN Operations

JOIN operations are used to combine rows from two or more tables based on a related column between them. Here are the common types of JOINs:

### INNER JOIN

The `INNER JOIN` keyword selects records that have matching values in both tables.

```sql
SELECT table1.column1, table2.column2
FROM table1
INNER JOIN table2
ON table1.common_column = table2.common_column;
```

### LEFT JOIN (or LEFT OUTER JOIN)

The `LEFT JOIN` keyword returns all records from the left table (table1), and the matched records from the right table (table2). The result is NULL from the right side if there is no match.

```sql
SELECT table1.column1, table2.column2
FROM table1
LEFT JOIN table2
ON table1.common_column = table2.common_column;
```

### RIGHT JOIN (or RIGHT OUTER JOIN)

The `RIGHT JOIN` keyword returns all records from the right table (table2), and the matched records from the left table (table1). The result is NULL from the left side when there is no match.

```sql
SELECT table1.column1, table2.column2
FROM table1
RIGHT JOIN table2
ON table1.common_column = table2.common_column;
```

### FULL JOIN (or FULL OUTER JOIN)

The `FULL JOIN` keyword returns all records when there is a match in either left (table1) or right (table2) table records. It returns NULL for the records of the table that does not have a match.

```sql
SELECT table1.column1, table2.column2
FROM table1
FULL JOIN table2
ON table1.common_column = table2.common_column;
```

### CROSS JOIN

The `CROSS JOIN` keyword returns the Cartesian product of the two tables. This means that it will return all possible combinations of rows.

```sql
SELECT table1.column1, table2.column2
FROM table1
CROSS JOIN table2;
```

### SELF JOIN

A `SELF JOIN` is a regular join but the table is joined with itself.

```sql
SELECT a.column1, b.column2
FROM table_name a, table_name b
WHERE condition;
```

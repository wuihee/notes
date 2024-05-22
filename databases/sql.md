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

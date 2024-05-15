# Databases

## Relational Databases

- **Definition**: Relational databases store data in tables and *relate* data between tables through foreign keys.
- **Structure**:
  - **Tables**: Comparable to an Excel sheet.
  - **Rows (Tuples / Records)**: Each row represents a single record.
  - **Columns (Attributes)**: Each column represents a data field within the record.
  - **Entries**: All the information in one row constitutes an entry.

## Structured Query Language (SQL)

- **Definition**: SQL is a *declarative* language, meaning you describe the data you want without specifying how to retrieve it.

### Data Definition Language (DDL)

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

### Data Manipulation Language (DML)

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

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
- **Example**:

```sql
CREATE TABLE table_name(
    column1 datatype PRIMARY KEY,
    column2 datatype,
    ...
);
```

### Select

```sql
SELECT * FROM table_name;
```

### Distinct

- Make sure we don't get duplicate sets/

```sql
SELECT DISTINCT name FROM students;
```

### Where

```sql
SELECT * FROM animals WHERE rating > 5;
SELECT * FROM animals WHERE type = "mammal";
```

### AND / OR

```sql
SELECT * FROM animals WHERE rating > 5 AND type = "mammal";
SELECT * FROM animals WHERE rating > 5 OR type = "mammal";
```

### Patterns

- Wildcard character `%` includes any characters.

```sql
SELECT * FROM animals WHERE description LIKE "%furry%";
```

# SQLite

- SQLite is a C-language library that provides a lightweight, disk-based database. Unlike other databases, it does not have a separate server process.
- Disk-based meaning data is stored on the disk as opposed to in memory (RAM).

## Installation

```bash
npm install sqlite sqlite3
```

## SQLite in Node.js

### Creating a Database Connection

```javascript
const sqlite3 = require("sqlite3");
const sqlite = require("sqlite");

async function getDBConnection() {
  const db = await sqlite.open({
    filename: "table.db",
    driver: sqlite3.Database
  });
  return db;
}
```

### `all()`

- Retrieves all rows from the result of an SQL query.
- Returns an array of objects, where each object represents a row.
- **Example**:

```javascript
(async () => {
  const db = await getDBConnection();
  const rows = await db.all("SELECT id, name, email FROM users");
  console.log(rows);
  await db.close();
})();
```

- **Output**:

```javascript
[
  { id: 1, name: 'Alice', email: 'alice@example.com' },
  { id: 2, name: 'Bob', email: 'bob@example.com' }
]
```

### `get()`

- Retrieves a single row from the result of an SQL query.
- Returns a single object representing the first row.
- **Example**:

```javascript
(async () => {
  const db = await getDBConnection();
  const row = await db.get("SELECT id, name, email FROM users WHERE id = ?", [1]);
})
```

- **Output**:

```javascript
{ id: 1, name: 'Alice', email: 'alice@example.com' }
```

### `exec()`

- Executes a batch of SQL queries without returning any rows.
- Useful for running multiple queries in one go and typcially used for schema changes or bulk updates.
- **Example**:

```javascript
(async () => {
  const db = await getDBConnection();
  await db.exec(`
    CREATE TABLE IF NOT EXIST orders (
      id INTEGER PRIMARY KEY AUTOINCREMENT,
      product TEXT,
      quantity INTEGER
    );
    INSERT INTO orders (product, quantity) VALUES ('Product 1', 10);
    INSERT INTO orders (product, quantity) VALUES ('Product 2', 20);
  `);
  await db.close();
})
```

### `run()`

- Executes a single SQL statement without returnig any rows.
- Returns information about the operation.
- **Example**:

```javascript
(async () => {
  const db = await getDBConnection();
  let result = await db.run("INSERT INTO users (name, email) VALUES (?, ?)", ["Charlie", "charlie@example.com"]);
  console.log(`Last inserted row ID: ${result.lastID}`);
  await db.close();
})
```

- **Output**:

```text
Last inserted row ID: 3
```

## Parameterized Queries

- Prevents SQL injections and allows data to be dynamically inserted into SQL queries.
- **Question Mark Placeholder (?)**: Place holder for the parameter.
- **Parameters Array**: The values to substitute into the placeholders.

```javascript
db.get("SELECT id, name, email FROM users WHERE name = ? AND email = ?", ["Alice", "alice@example.com"]);
```

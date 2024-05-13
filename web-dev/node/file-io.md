# File I/O

## `fs` Core Module

```javascript
const fs = require("fs");
```

- [`fs.readFile(path, callback)`](https://nodejs.org/api/fs.html#fsreadfilepath-options-callback): Asynchronously read the contents of a file.

```javascript
fs.readFile("/path/file.txt", (err, data) => {
  if (err) {
    console.error(err);
  } else {
    console.log(data)
  }
})
```

- [`fs.writeFile(path, data, callback)`](https://nodejs.org/api/fs.html#fswritefilefile-data-options-callback): Asynchronously write the contents of a file and replaces the current contents.

```javascript
fs.writeFile("/path/file.txt", "new content", (err) => {
  if (err) {
    console.error(err);
  } else {
    console.log("Success!");
  }
})
```

## Promise-Based `fs`

- We can omit the use of callback by using `Promises`.

```javascript
const fs = require("fs/promises")

async function readFile() {
  try {
    let data = await fs.readFile("file.txt");
    console.log("File contents: " + data);
  } catch (err) {
    console.error(err);
  }
}
```

## Backend Example

- `if (err.code === "ENOENT")`: Unable to find file.

```javascript
const express = require("express");
const fs = require("fs/promises");

app.get("/read", async (req, res) => {
  try { 
    let data = await fs.readFile("file.json");
    data = JSON.parse(data);
    res.json(data);
  } catch (err) {
    if (err.code === "ENOENT") {
      res.type("text").status(500).send("File not found.");
    } else {
      res.type("text").status(500).send("Server error.");
    }
  }
})
```

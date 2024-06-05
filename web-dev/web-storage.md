# Web Storage

- `sessionStorage`: Persists data only for the duration of the page session. Data is lost when the session ends, i.e. when the page is closed.

```javascript
// Save data to sessionStorage
sessionStorage.setItem("key", "value");

// Get saved data from sessionStorage
let data = sessionStorage.getItem("key");

// Remove saved data from sessionStorage
sessionStorage.removeItem("key");

// Remove all saved data from sessionStorage
sessionStorage.clear();
```

- `localStorage`: Persists data indefinitely, even after the browser is close. Data is retained until explicitly deleted.

```javascript
// Save data to localStorage.
localStorage.setItem("key", "value");

// Get saved data from localStorage.
let data = localStorage.getItem("key");

// Remove saved data from localStorage.
localStorage.removeItem("key");

// Remove all saved data from localStorage.
localStorage.clear();
```

- Both `sessionStorage` and `localStorage` store data as strings. To store, objects or arrays, we need to serialize them using `JSON`.

```javascript
let user = { name: "John", age: 30 };

// Serialize object to JSON string and store
localStorage.setItem("user", JSON.stringify(user));

// Retrieve and deserialize JSON string back to object
let retrievedUser = JSON.parse(localStorage.getItem("user"));
```

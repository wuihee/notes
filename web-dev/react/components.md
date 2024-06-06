# Components

- Components are JavaScript functions that return re-usable UI elements, typically written in JSX.

  ```javascript
  function HelloWorld() {
    return (
      <h1>Hello, World!</h1>
    );
  }
  ```

- Components can then be used within other components.

  ```javascript
  function App() {
    return (
      <HelloWorld />
    );
  }
  ```

## Importing & Exporting Components

- We can split our components into different files and export them using *default* or *named* exports.

  `navbar.js`

  ```javascript
  default export function Navbar() {
    return (
      <nav>
        <a href="">About</a>
        <a href="">Home</a>
        <a href="">Contact</a>
      </nav>
    );
  }
  ```

  `header.js`

  ```javascript
  export function Title() {
    return (
      <h1>Title</h1>
    );
  }
  ```

  `app.js`

  ```javascript
  import Navbar from "./navbar";  // Default export.
  import {Title} from "./title";  // Named export.
  ```

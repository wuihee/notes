# JSX

- JSX is a syntax extension for writing HTML-like markup within JavaScript.
- Under the hood, it is syntactic sugar which uses React's `createElement` function to generate HTML elements.

## JSX Rules

- **Only return a single root element**. An empty tag `<></>`, called a *fragment*, can be used to wrap elements.

  ```javascript
  function App() {
    return (
      <>
        <h1>My Website</h1>
        <Contents />
      </>
    );
  }

  function Contents() {
    return (
      <p>Contents of my website...</p>
    );
  }
  ```

- Close all tags.

  ```javascript
  function App() {
    return (
      <input />  // Not <input>.
    )
  }
  ```

- **Mostly use camel case.** This is because JSX is converted into JavaScript and identifiers like `class` are reserved keywords.

  ```javascript
  function App() {
    return (
      <h1 className="title" textDecoration="underline">My Website</h1>
    );
  }
  ```

## Using JavaScript in JSX

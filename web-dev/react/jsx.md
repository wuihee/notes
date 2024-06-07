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

- We can dynamically specify the contents of JSX by opening a window into JavaScript using curly braces (just like f-strings in Python).
- **Specify Attributes**:

  ```javascript
  function App() {
    let avatar = "imgs/avatar.png";
    let description = "This is an avatar image";

    return (
      <img
        className="avatar"
        src={avatar}
        alt={description}
      />
    );
  }
  ```

- **Specify Text**:

  ```javascript
  function App() {
    let title = "My Website":
    return (
      <h1>{title}</h1>
    );
  }
  ```

### Double Curlies

- We can pass in objects into JSX using double curlies. This is usually used to specify inline CSS.

  ```javascript
  function App() {
    return (
      <ul style={{
        backgroundColor: 'black',
        color: 'pink'
      }}>
        <li>Math Homework</li>
        <li>CS Homework</li>
        <li>Wank</li>
      </ul>
    );
  }
  ```

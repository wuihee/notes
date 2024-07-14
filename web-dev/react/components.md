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

## Passing Data to Components

- We can specify arguments for our components as if they were functions, which we do using the `props` object.

    ```javascript
    function Button(props) {
        const buttonStyle = {
            color: props.color,
            fontSize: props.fontSize + "px"
        };
        return (
            <button style={buttonStyle}>{props.text}</button>
        );
    }

    export default function App() {
        return (
            <Button text="click me!" color="red" fontSize={13} />
            <Button text="click me too!" color="blue" fontSize={14} />
        );
    }
    ```

- We can be more concise in our syntax using destructuring.

    ```javascript
    function Button({ color, fontSize, label }) {
        const buttonStyle = {
            color: color,
            fontSize: fontSize + "px"
        };
        return (
            <button style={buttonStyle}>{props.label}</button>
        );
    }
    ```

- We can specify default values for props.

    ```javascript
    Button.defaultProps = {
        text: "click me!",
        color: "green",
        fontSize: 12
    }

    export default function App() {
        return (
            <Button />
            <Button text="click me too!" fontSize={14} />
        );
    }
    ```

- We can also pass in functions into `props`.

    ```javascript
    function Button({ handler }) {
        return (
            <button onclick={handler}>Go to Link!</button>
        );
    }

    export default function App() {
        const handler = () => window.location.href("www.youtube.com");
        return (
            <Button handler={handler} />
        );
    }
    ```

### Passing JSX as Children

- It is possible to nest components:

  ```javascript
  <Parent>
    <Child />
  </Parent>
  ```

- The parent component, `Parent`, will receive the child component, `Child` in a prop called `children`. We can then render the child like so.

  ```javascript
  function Parent({ children }) {
    return (
      <div>
        {children}
      </div>
    )
  }
  ```

## Keeping Components Pure

- Components should be like math functions - given the same input, they should always have the same output, with no *side effects*.
- A side effect occurs when some external thing is changed.
- In *strict mode*, React renders components twice to catch errors and make sure nothing changes with multiple renders.

## UI as a Tree

- React models the relationship between components as a tree, like the DOM.
- It also does the same for imports.

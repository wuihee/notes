# Event Handling

## Event Propagation

- Event propagation occurs when multiple elements along the DOM tree contain event handlers that respond and then propagate.
  - E.g. A `<button>` contained in a `<div>` where both have `onClick` event handlers.
- The most nested event handler will activate first, then propagate upwards.

### Stopping Propagation

- Event propagation can be stopped using the `event` object that is passed to the event handler function.

    ```js
    function Button({ onClick, children }) {
    return (
      <button onClick={e => {
        e.stopPropagation();
        onClick();
      }}>
        {children}
      </button>
      );
    }
    ```

## Preventing Default Behavior

- Some browser events have default behavior associated with them, such as the `<form>` submit event which reloads the page.
- We can prevent this by using `e.preventDefault()`.

  ```js
  function SignUp() {
    return (
      <form onSubmit={e => {
        e.preventDefault();
        alert("Submitting!");
      }}>
        <input />
        <button>Submit</button>
      </form>
    );
  }
  ```

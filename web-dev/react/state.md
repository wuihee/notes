# State

- Components need to be updated respond to user events. The problem is:
  - Local variables don't persist between renders.
  - Changes to local variables won't trigger renders.
- Every time React re-renders components are destroyed and rebuilt.
- Therefore we need to:
  - *Retain* data between renders.
  - *Trigger* React to re-render components.

## Hooks

- In React, any function starting with "`use`", is a *Hook*.
- Hooks are special functions that are only available while React is rendering.
- They can only be used at the top of your components, like an import statement.

## `useState` Hook

- The `useState` hook provides:
  - A *state variable* to retain data between renders.
  - A *state setter function* to update the variable and trigger re-rendering.

    ```javascript
    import { useState } from 'react';

    const [stateValue, setStateFunction] = useState(initialValue);
    ```

- E.g.

    ```javascript
    import { useState } from 'react';

    export default function CoolButton() {
        const COLORS = ["red", "green", "blue"];
        const [color, setColor] = useState(0);

        function handleClick() {
            setColor((color + 1) % COLORS.length);
        }

        return (
            <>
                <button style={{ backgroundColor: COLORS[color] }} onClick={handleClick}>
                    Change Color
                </button>
            </>
        );
    }
    ```

- A component can have multiple state variables.
- State is also isolated to each component instance. So two different instances of the same component will not share the same state.

### How Does React Know Which State to Use?

- States are basically stored in an array.
- When we re-render a component from scratch, our hook "imports" will be in the same order. So we can iterate through the array in the same order and get our correct hooks.
- Below is a mock implementation.

    ```javascript
    let hooks = [];
    let i = 0;

    function useState(initialState) {
        let pair = hooks[i];

        if (pair) {
            i++;
            return pair;
        }

        pair = [initialState, setState];

        function setState(newState) {
            pair[0] = newState;
            render();
        }

        hooks[i] = pair;
        i++;
        return pair;
    }

    function render() {
        i = 0;
        // Plus other stuff to render the components.
    }

    export default function App() {
        let [count, setCount] = useState(0);

        function handleClick() {
            setCount(count + 1);
        }
        return (
            <>
                <button onClick={handleClick}>Click Me {count}</button>
            </>
        );
    }
    ```

## Rendering

- Rendering consists of three steps:
  1. *Triggering* the render.
  2. *Rendering* the component.
  3. *Committing* to the DOM.
- React components render when:
  - When the app starts.

    ```javascript
    import Image from './Component.js';
    import { createRoot } from 'react-dom/client';

    const root = createRoot(document.getElementById("root"));
    root.render(
        <Component />
    )
    ```

  - The other time that components render is when `setState` functions are called.
- After rendering, React will update the DOM.
  - For the initial render React will use the `appendChild` DOM API.
  - Subsequently, it will do fancy calculations to update only the necessary elements.

### Reconciliation Algorithm

- The reconciliation algorithm is the algorithm which React uses to efficiently update components.
- **Tree Diffing**: React uses a virtual DOM to first update the UI and then compares it to the actual DOM and calculates the minimum changes needed to be made.
- **Batching**: React batches multiple changes into a single update which reduces the number of updates to the virtual DOM, and in turn, the real DOM.

## State as a Snapshot

- When ever the `useState` function in a component is called, a re-render is triggered.
- The component the returns a *snapshot* of the JSX with the current *state*. The component's state actually lives in React's backend.

    ```js
    import { useState } from 'react';

    export default function Counter() {
        let [number setNumber] useState(0);

        return (
            <>
                <h1>{number}</h1>
                <button onClick={() => {
                    setNumber(number + 1);
                    setNumber(number + 1);
                    setNumber(number + 1);
                }}>+3</button>
            </>
        )
    }
    ```

- In the example below, when the button is clicked, `number` will only display 1, and not 3. This is because setting state only changes `number` for the next render - in each call to `setNumber(number + 1)`, React doesn't update the state immediately, but prepares to change `number` to 1 on the next render.

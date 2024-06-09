# Rendering Techniques

## Conditional Rendering

- Ternary operator.

    ```javascript
    return (
        <li className="item">
            {isPacked ? name + ' ✔' : name}
        </li>
    );
    ```

- Logical AND Operator (`&&`). Left side of `&&` should always be a boolean condition and not a number like 0. Otherwise JavaScript will return the number.

    ```javascript
    return (
        <li className="item">
            {name} {isPacked && '✔'}
        </li>
    );
    ```

- Using basic conditions.

    ```javascript
    let itemContent = name;
    if (isPacked) {
        itemContent = name + ' ✔'; 
    }
    return (
        <li className="item">
            {itemContent}
        </li>
    );
    ```

## Rendering Lists

- We can render lists by using the `map` function to construct a list of `<li>` objects.

    ```javascript
    function App() {
        const animals = ["Lion", "Cow", "Snake", "Lizard"];
        return (
            <div>
                <h1>Animals: </h1>
                <ul>
                    {animals.map(animal => (
                        <li key={animal}>{animal}</li>
                    ))}
                </ul>
            </div>
        );
    }
    ```

### `key`

- JSX elements inside a `map()` call always need a unique key. This is so that React has a unique way to reference these elements instead of referring to them by their order, which may change later on.
- The `uuid` package can be used to generate unique keys.

    ```javascript
    const todos = [
        { task: "Math HW", id: uuid() },
        { task: "CS HW", id: uuid() },
        { task: "English HW", id: uuid() },
    ]

    function TodoList() {
        return (
            <ul>
                {todos.map(todo => (
                    <li key=todo.id>{todo.task}</li>
                ))}
            </ul>
        );
    }
    ```

### Rules of Keys

- Keys must be unique among their siblings.
- Keys must not change. This means do not generate them while rendering.

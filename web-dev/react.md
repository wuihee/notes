# React

## Framework vs Library

- Frameworks and libraries are both code written by other people to make your life easier.
- A framework *inverts the control* of a program and tells the programmer what to do within the framework they provide.
- A library allows the programmer to pick and choose the functions they want to use.
- The degree of freedom in a library or framework is how *opinionated* it is.

## Content Delivery Network (CDN)

- A bunch of servers spread across the world that provide fast resources for people.

## Creating a React Project

- Package Management (NPM, Yarn)
- Module Bundling (Webpack, Parcel)
- Compilation (Babel)
- React

## Vite

- Vite is a front-end build tool that simplifies a lot of things.
- Scaffold a new React project.

```bash
npm create vite@latest my-first-react-app -- --template react
```

- Run project.

```bash
npm run dev
```

## Components

```javascript
function HelloWorld() {
    return (
        <h1>Hello, World!</h1>
    );
}
```

## JSX

- JSX is syntactic sugar for the React `createElement` function, which allows us to write HTML like code in JavaScript.
- In JSX we can only return a single root element. An empty tag is called a *fragment*.

```javascript
function App() {
    return (
        <>
            <h1>Example 1</h1>
            <h2>Example 2</h2>
        </>
    );
}
```

- All tags must be closed.

```javascript
function App() {
    return (
        <>
            <input />
            <li></li>
        </>
    );
}
```

- Camel case most attributes. This is because JSX is converted into JavaScript and identifiers like `class` are reserved keywords.

```javascript
function App() {
    return (
        <>
            <h1 className="eg" strokeWidth="2">Example</h1>
        </>
    );
}
```

### Using JavaScript in JSX

- We can open a window into JavaScript in JSX by using curly braces, just like Python's f-strings.

```javascript
export default function App() {
    return (
        <h1 className={titleClass}>{title}</h1>
    );
}
```

- We can also pass objects into JSX using double curly braces.

```javascript
export default function App() {
    return (
        <div style={{
            backgroundColor: 'black',
            color: 'pink'
        }}></div>
    );
}
```

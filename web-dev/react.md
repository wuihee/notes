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

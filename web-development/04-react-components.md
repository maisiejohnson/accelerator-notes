# REACT: COMPONENTS

## Frameworks

- React is a **framework**/ **library**.
- A framework is a set of pre defined interfaces, functions and concepts that help developers build immersive and engaging user interfaces.

## Importing React

- To create a react component, we first need to import react:
  ```JSX
  import React from 'react';
  ```
- This creates an object named `React`, which contains methods necessary to use the React library.
- React is imported from the 'react' package, which should be installed in your project as a dependency.

## Importing ReactDOM

- Another import we need in addition to React is `ReactDOM`
- The methods imported from 'react-dom' interact with the DOM.
- The methods imported from 'react' do not deal with the DOM at all. They don’t engage directly with anything that isn’t part of React.
- To import `ReactDom` add the following line of code:
  ```JSX
  import ReactDOM from 'react-dom/client';
  ```

## Components

- React applications are made of **components**.
- A component is a small, reusable chunk of code that is responsible for one job. That job is often to render some HTML and re-render it when some data changes.
- Components are defined as **functions**.
- When we define a functional component, we essentially define a factory that can build the appropriate combination of elements every time we reference its name. It builds it by consulting a set of instructions that you must provide.
- Function component names must start with capitalization and are conventionally created with **PascalCase**.
- Due to how JSX tags are compiled, capitalization indicates that it is a React component rather than an HTML tag.
- React function components must contain a `return` statement. This should return some React elements created with JSX.

  ```JSX
  import React from 'react';

  function MyComponent() {
      return <h1>Hello, this is a function component.</h1>;
  }
  ```

- Function components can contain JSX, and logic in the function body before the return statement.
- You can also have event listeners and event handlers inside a component.

## Importing and Exporting React Components

- A React application typically has two core files: `App.jsx` and `index.jsx`. The `App.jsx` file is the top level of your application, and `index.jsx` is the entry point.
- If you define a component inside of App.js, we have to export it to `index.jsx` to render because `index.jsx` is the entry point.
- To export them, we can prefix it with the `export` declaration and specify if it is a default or named export.
- For example, after the function component definition, in `App.jsx`, we can default export our component like so:
  ```JSX
  export default MyComponent;
  ```
- To import the component into `index.jsx`:
  ```JSX
  import MyComponent from './App';
  ```

## Using and Rendering a Component

- We can use a **function component** with an HTML-like syntax that resembles a self-closing tag:
  ```JSX
  <MyComponent />
  ```
- If you need to nest other components in between, you may also use an opening and corresponding closing tag structure:
  ```JSX
  <MyComponent>
      <OtherComponent />
  </MyComponent>
  ```
- To render our component to the browser, we must rely on the .createRoot() and .render() methods from the react-dom library. This should be done in our entry point, index.js.
- For example:
  ```JSX
  ReactDOM.createRoot(document.getElementById('app')).render(<MyComponent />);
  ```
  - `document.getElementById('app')` returns a DOM element from index.html.
  - `.createRoot()` receives the DOM element as the first argument and creates a root for it.
  - `.createRoot()` returns a reference to the root container on which you can call methods like `.render()`.

## Props

- Components can interact by passing information into each other
- Information that gets passed from one component to another is called **props**
- Props can be used to customize the output of each component depending on the information that is passed in
- A component’s `props` is an object that holds information about that component.
- To access a component’s `props` object, you can reference the props object and the dot notation for its properties. E.g.,

  ```JSX
  props.name
  ```

  - This would retrieve the `name` property from the `props` object.

- To use props, pass props in as a parameter when defining a function component. For example:

  ```JSX
  const MyComponent = (props) => {
      return <h1>Hello, my name is {props.name}</h1>
  }

  <MyComponent name="Maisie"/>
  ```

- To take advantage of props, we need to pass information to a React component, which we do by giving the component an attribute.
- If you want to pass information that isn’t a string, then wrap that information in curly braces.
  ```JSX
  <Greeting name="The Queen Mary" city="Long Beach, California" age={56} haunted={true} />
  // age and haunted props aren't strings so we wrap them in curly braces
  ```
- Props are passed from component to component downwards. That is, props are passed down from parent components to child components.

### `props.children`

- Every component’s `props` object has a property named `children`
- `props.children` will return everything in between a component’s opening and closing JSX tags.
- By using props.children, we can separate the outer component from the content which makes it flexible and reusable.
- If a component has more than one child between its JSX tags, then `props.children` will return those children in an array. However, if a component has only one child, then `props.children` will return the single child, not wrapped in an array.

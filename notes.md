<!-- Ouestion 1 : Difference between Element and Component -->

Definition
Element: A React Element is a plain JavaScript object that describes what you want to appear on the screen. It is immutable and represents a DOM node or another component. Elements are the smallest building blocks in React.

Component: A React Component is a function or class that returns JSX (or React elements). It allows you to split the UI into independent, reusable pieces and manage their logic, state, and behavior.

Example
React Element (Without JSX):

const element = React.createElement("div", { id: "login-btn" }, "Login");

Equivalent JSX:

<div id="login-btn">Login</div>
What React.createElement() returns:

{
  type: 'div',
  props: {
    id: 'login-btn',
    children: 'Login'
  }
}
React Component (Functional):

jsx
Copy
Edit
const Button = ({ handleLogin }) => (
  <div id="login-btn" onClick={handleLogin}>
    Login
  </div>
);

JS equivalent of above JSX:

const Button = ({ handleLogin }) =>
  React.createElement(
    "div",
    { id: "login-btn", onClick: handleLogin },
    "Login"
  );

How to Tell in an Interview
"In React, an element is a plain JavaScript object that describes a DOM node or another component. It’s immutable and created using React.createElement() or JSX. A component, on the other hand, is a function or class that returns JSX. Components are reusable, can handle state, and represent a piece of UI logic. While elements are what React uses to build the virtual DOM, components are how we structure and organize the UI."
<!-- ------------------------------------------------------------------------------------------------------------------------------------- -->

<!-- Question 2 :How to Create Components -->

Definition
Components are the core building blocks of a React application. They let you split the UI into independent, reusable pieces. React offers two main ways to define components:

Function Components: These are simple JavaScript functions that receive props and return JSX. They are the most commonly used method, especially with Hooks.

Class Components: These are ES6 classes that extend React.Component and must include a render() method. They were widely used before Hooks were introduced.

Example
Function Component:

function Greeting({ message }) {
  return <h1>{`Hello, ${message}`}</h1>;
}
Class Component:

class Greeting extends React.Component {
  render() {
    return <h1>{`Hello, ${this.props.message}`}</h1>;
  }
}
Both will render:

<h1>Hello, [message]</h1>

How to Tell in an Interview
"In React, we can create components either as function components or class components. Function components are preferred today because they're simpler and support Hooks for state and lifecycle features. They accept props as input and return JSX. Class components are ES6 classes that extend React.Component and include a render() method. Although still valid, class components are now less commonly used in new codebases."


<!-- --------------------------------------------------------------------------------------------------------------------------------------- -->

<!-- Question 3:  What is State? -->

Definition
State in React is a built-in object used to store dynamic data in a component. It determines how that component behaves and what it renders. Unlike props, which are passed down from parent to child, state is local and controlled within the component. When the state changes, React automatically re-renders the component to reflect the new values.

import { useState } from "react";

function User() {
  const [message, setMessage] = useState("Welcome to React world");

  return (
    <div>
      <h1>{message}</h1>
    </div>
  );
}
useState("Welcome to React world") initializes state.

message is the current state value.

setMessage is the function used to update the state.

When setMessage is called, the component re-renders with the updated state.

How to Tell in an Interview
"In React, state is a built-in object used to manage data that can change over the lifetime of a component. It's local to the component and can be initialized using the useState Hook in function components. Whenever the state changes, React re-renders the component with the new state. This is how React maintains interactivity and ensures the UI stays in sync with user actions or application logic."

<!-- ----------------------------------------------------------------------------------------------------------------------------------- -->

<!-- Question 4: What is Virtual DOM? -->


Definition
The Virtual DOM (VDOM) is a lightweight JavaScript representation of the real DOM in the browser. Instead of directly manipulating the browser's DOM (which is slow), React creates a virtual copy of the DOM in memory. When the state of a component changes, React updates the Virtual DOM first, compares it with the previous version (using a process called diffing), and then efficiently updates only the parts of the real DOM that changed.

Example
Let's say a component renders a list of items:

function ItemList({ items }) {
  return (
    <ul>
      {items.map(item => <li key={item.id}>{item.name}</li>)}
    </ul>
  );
}
Initially, the Virtual DOM contains a tree structure representing this list.

If one item changes, React:

Updates the Virtual DOM.

Compares it with the old Virtual DOM.

Updates only that changed <li> in the real DOM instead of re-rendering the whole <ul>.

How to Tell in an Interview
"The Virtual DOM is a concept used by React to optimize performance. Instead of manipulating the real DOM directly, React keeps a virtual copy of the UI in memory. When changes occur, React performs a diffing algorithm to compare the new Virtual DOM with the previous one, and then applies only the minimal required changes to the actual DOM. This process makes updates faster and more efficient, leading to better performance in complex applications."

<!-- ----------------------------------------------------------------------------------------------------------------------------------------->

<!-- Question 5: What are Stateful Components?-->
Definition
A stateful component in React is a component whose behavior and rendered output depend on its internal state. These components manage their own data using React's useState Hook (for function components) or this.state (in class components). The state allows the component to respond to user input, server responses, or other changes dynamically.

Example

import React, { useState } from 'react';

const App = () => {
  const [count, setCount] = useState(0);

  const handleIncrement = () => {
    setCount(count + 1);
  };

  return (
    <>
      <button onClick={handleIncrement}>Increment</button>
      <span>Counter: {count}</span>
    </>
  );
};
useState(0) initializes the count state to 0.

handleIncrement updates the state on button click.

Since the component depends on and updates state, it is stateful.

How to Tell in an Interview
"A stateful component is one that maintains its own state using either the useState hook in function components or this.state in class components. These components re-render automatically whenever their state changes. They’re useful when you need to track data that updates over time—like form inputs, counters, or toggle buttons. In contrast, stateless components simply receive data via props and don’t manage internal state." 

<!-- ---------------------------------------------------------------------------------------------------------------------------------- -->

<!-- Question 6: How to Loop Inside JSX -->
Definition
In JSX, you cannot use traditional control statements like for loops directly inside the return block because JSX is syntactic sugar for function calls and expressions, not statements. Instead, the most common and recommended way to loop in JSX is by using JavaScript’s Array.prototype.map() method, which works perfectly inside JSX expressions.

Example
✅ Correct way using map():

<tbody>
  {items.map((item) => (
    <SomeComponent key={item.id} name={item.name} />
  ))}
</tbody>

❌ Incorrect way using for loop (will cause an error):
<tbody>
  for (let i = 0; i < items.length; i++) {
    <SomeComponent key={items[i].id} name={items[i].name} />
  }
</tbody>

The map() method is used because it returns an array of elements, which is exactly what JSX expects inside expressions.

You must use a unique key prop when rendering lists in React for optimal rendering performance and correct DOM diffing.

How to Tell in an Interview
"In JSX, we use the map() method to loop over arrays because JSX expects expressions, not statements like for loops. map() lets us transform an array of data into an array of elements that can be rendered. For example, when rendering a list of components, we pass each item to map() and return a JSX element with a unique key prop. Using traditional loops like for directly inside JSX will result in a syntax error because JSX doesn't support statement blocks." 

<!-- ------------------------------------------------------------------------------------------------------------------------------------ -->

<!-- Question 7 :Difference between React and ReactDOM  -->

Definition

React: The react package provides the core functionalities of the React library. It includes functions and classes like React.createElement(), React.Component, useState, and useEffect, which are used to build and manage components and elements. It's platform-agnostic, meaning it doesn’t assume anything about the environment (browser, server, native).

ReactDOM: The react-dom package is specific to web browsers. It provides methods to interact with the DOM, like ReactDOM.render() for rendering components to the browser, and ReactDOM.hydrate() for hydration in SSR (server-side rendering). It acts as a bridge between React and the actual DOM.

Example
// react
import React, { useState } from 'react';

// react-dom
import ReactDOM from 'react-dom/client';

// Create a simple component
function App() {
  const [message] = useState("Hello React");
  return <h1>{message}</h1>;
}

// Render to the DOM
const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(<App />);
useState comes from react

ReactDOM.createRoot and render come from react-dom

How to Tell in an Interview
"React provides the core APIs like createElement, Hooks, and component classes that we use to build components, but it doesn’t deal with the DOM directly. ReactDOM, on the other hand, provides the methods needed to render those components into the actual DOM in web browsers, such as ReactDOM.render() or ReactDOM.createRoot(). So React is about building components, and ReactDOM is about mounting them to the browser."

<!-- -------------------------------------------------------------------------------------------------------------------------------------- -->

<!-- Question 8:What is React Router? -->

Definition

React Router is a standard routing library for React applications. It enables navigation between different views or pages in a single-page application (SPA) without reloading the entire page. React Router uses dynamic routing, meaning the routing is handled as part of the component rendering, allowing seamless navigation and deep linking within the app.

It provides components like <BrowserRouter>, <Routes>, <Route>, <Link>, and hooks like useNavigate, useParams, and useLocation to control navigation and access route-related data.

Example

import { BrowserRouter, Routes, Route, Link } from 'react-router-dom';

function Home() {
  return <h2>Home Page</h2>;
}

function About() {
  return <h2>About Page</h2>;
}

function App() {
  return (
    <BrowserRouter>
      <nav>
        <Link to="/">Home</Link>
        <Link to="/about">About</Link>
      </nav>
      <Routes>
        <Route path="/" element={<Home />} />
        <Route path="/about" element={<About />} />
      </Routes>
    </BrowserRouter>
  );
}
<BrowserRouter> wraps the app to enable routing.

<Route> defines the path-to-component mapping.

<Link> is used for navigation without full page reloads.

How to Tell in an Interview
"React Router is a popular library used for implementing routing in React single-page applications. It allows developers to map URLs to specific components and handle client-side navigation without reloading the page. It uses dynamic routing and provides various tools like <BrowserRouter>, <Route>, <Link>, and hooks like useNavigate for navigation and route management. This makes React apps feel fast and seamless, just like a native application."

<!-- ------------------------------------------------------------------------------------------------------------------------------------ -->

<!-- Question 9 :: What is Redux? -->

Definition
Redux is a state management library for JavaScript applications, commonly used with React. It provides a single centralized store to hold the entire application state and allows predictable state updates through pure functions called reducers. Redux follows a unidirectional data flow pattern: components dispatch actions, reducers process those actions, and the store updates the state accordingly.

Redux is useful in large-scale applications where managing state across many components becomes complex.

Example
A simple Redux flow:

// Action
const increment = () => ({ type: 'INCREMENT' });

// Reducer
const counterReducer = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT': return state + 1;
    default: return state;
  }
};

// Store
import { createStore } from 'redux';
const store = createStore(counterReducer);

// Dispatch
store.dispatch(increment());
console.log(store.getState()); // Output: 1


<!-- In a React app, we use react-redux for integration: -->

import { useDispatch, useSelector } from 'react-redux';

function Counter() {
  const count = useSelector(state => state);
  const dispatch = useDispatch();

  return (
    <>
      <button onClick={() => dispatch({ type: 'INCREMENT' })}>Increment</button>
      <p>Count: {count}</p>
    </>
  );
}

How to Tell in an Interview
"Redux is a predictable state container for JavaScript applications, often used with React for centralized state management. It helps manage state in large applications by storing the entire state in a single store. State changes in Redux are handled via pure functions called reducers, which respond to actions dispatched by components. Redux follows a unidirectional data flow, making the app's state more predictable and easier to debug." 

<!-- =---------------------------------------------------------------------------------------------------------------------------------- -->

<!-- Question 10:Difference between React Context and Redux -->

Definition
Both React Context and Redux are tools for managing state in React applications, but they serve different use cases and operate differently:

React Context is a built-in feature used to pass data deeply through the component tree without prop drilling. It’s ideal for simple or global data (like themes, user auth, locale).

Redux is a third-party library that provides a centralized store and a strict architecture for state management using actions, reducers, and middleware. It’s suited for complex, large-scale applications.

<!-- ---------------------------------------------------------------------------------------------------------------------------------- -->

<!-- Question 11: What are Hooks  -->

Hooks are special functions introduced in React 16.8 that let you use state and other React features in functional components, which previously were only available in class components. Hooks allow you to manage state, handle side effects, access context, and more — all without writing a class.

Commonly used built-in Hooks:

useState() – for state management

useEffect() – for handling side effects (like data fetching or subscriptions)

useContext() – to consume context

useRef(), useReducer(), useMemo(), and others for advanced needs

Example

import React, { useState, useEffect } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    document.title = `Count: ${count}`;
  }, [count]); // Runs only when `count` changes

  return (
    <>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <p>Count: {count}</p>
    </>
  );
}
u
<!-- seState(0) initializes state. -->

<!-- useEffect() updates the page title whenever count changes. -->

<!-- ------------------------------------------------------------------------------------------------------------------------------------ -->

<!-- Question 12: Difference Between Real DOM and Virtual DOM  -->

Definition
Real DOM (Document Object Model) is the actual structure of the web page rendered by the browser. When changes are made, the entire DOM may need to be updated and re-rendered, which is slow and resource-intensive.

Virtual DOM is a lightweight, in-memory representation of the real DOM used by React. When the UI changes, React updates the Virtual DOM first, compares it with the previous version (diffing), and applies only the necessary updates to the real DOM. This makes updates faster and more efficient.

Example

Feature          	Real DOM	                Virtual DOM
Update Speed	      Slow	                      Fast
DOM Manipulation	Expensive	                  Optimized & Efficient
Direct HTML Update	Yes	                          No (via React rendering only)
Memory Usage	    High (with many updates)	  Minimal
Update Strategy	    Re-renders entire DOM tree	   Diffs and patches only changes

Real DOM Example:

document.getElementById('root').innerHTML = '<h1>Hello</h1>';

Virtual DOM (React) Example:

ReactDOM.render(<h1>Hello</h1>, document.getElementById('root'));

How to Tell in an Interview
"The Real DOM is the browser's actual document structure. Every time a change is made, the entire DOM may be re-rendered, which can be slow. In contrast, Virtual DOM is a concept used by React to improve performance. React creates a virtual copy of the DOM in memory, updates it when state or props change, and then efficiently applies only the differences to the real DOM using a process called reconciliation. This makes UI updates faster and more efficient, especially in large applications."


<!-- ------------------------------------------------------------------------------------------------------------------------------------- -->

<!-- Question 13: How to Fetch Data with React Hooks -->

Definition
To fetch data in React using hooks, we use the useEffect hook for executing side effects (like data fetching), and the useState hook to store and manage the fetched data. The useEffect hook allows you to run asynchronous code when the component mounts or updates. When an empty dependency array [] is passed, the effect runs only once — similar to componentDidMount() in class components.

Example
✅ Using fetch() API:

import React, { useEffect, useState } from "react";

function App() {
  const [data, setData] = useState({ hits: [] });

  useEffect(() => {
    fetch("https://hn.algolia.com/api/v1/search?query=react")
      .then((response) => response.json())
      .then((data) => setData(data));
  }, []); // Empty dependency array: runs once on mount

  return (
    <ul>
      {data.hits.map((item) => (
        <li key={item.objectID}>
          <a href={item.url}>{item.title}</a>
        </li>
      ))}
    </ul>
  );
}

export default App;

✅ Using Axios (alternative):

<!-- npm install axios -->


import axios from "axios";
import React, { useEffect, useState } from "react";

function App() {
  const [data, setData] = useState([]);

  useEffect(() => {
    axios.get("https://hn.algolia.com/api/v1/search?query=react")
      .then((res) => setData(res.data.hits));
  }, []);

  return (
    <ul>
      {data.map((item) => (
        <li key={item.objectID}>
          <a href={item.url}>{item.title}</a>
        </li>
      ))}
    </ul>
  );
}

How to Tell in an Interview
"We use useEffect to fetch data in functional React components. It runs after the component renders, and when we pass an empty array as its second argument, it behaves like componentDidMount, meaning it only runs once on initial render. We typically fetch data using fetch() or libraries like Axios, and store the result using useState. This keeps data fetching and component logic clean and React-idiomatic."

<!-- --------------------------------------------------------------------------------------------------------------------------------- -->

<!-- Question 14:  Difference Between useState and useRef Hook -->

Definition
useState is a React Hook used to create and manage stateful values in a component. When the state changes, React re-renders the component.

useRef is a React Hook used to create a mutable reference that persists across renders without causing a re-render when its value changes. It’s commonly used to reference DOM elements or store values like previous state, timers, or external library instances.

Example

✅ useState Example (causes re-render):

import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <p>{count}</p>
    </>
  );
}

✅ useRef Example (no re-render):

import React, { useRef } from 'react';

function Timer() {
  const timerId = useRef(null);

  const startTimer = () => {
    timerId.current = setInterval(() => {
      console.log("Timer running...");
    }, 1000);
  };

  return <button onClick={startTimer}>Start Timer</button>;
}

How to Tell in an Interview
"useState is used when I want a value that, when updated, should trigger a re-render of the component. For example, tracking user input or counters. On the other hand, useRef holds a mutable value that persists across renders but doesn’t cause the component to re-render when updated. I typically use useRef for DOM manipulation, storing timer IDs, or keeping track of previous values."

<!-- --------------------------------------------------------------------------------------------------------------------------------- -->

<!-- Question 15:  -->
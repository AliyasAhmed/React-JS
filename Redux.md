# Redux Usage Summary

### Install Redux Toolkit and React-Redux

#### Add the Redux Toolkit and React-Redux packages to your project:

```jsx
npm install @reduxjs/toolkit react-redux
```

# Create a Redux Store

Create a file named `src/redux/store.js.` Import the configureStore API from Redux Toolkit. We'll start by creating an empty Redux store, and exporting it:

```jsx
src / redux / store.js;

import { configureStore } from "@reduxjs/toolkit";

export default configureStore({
  reducer: {},
});
```

This creates a Redux store, and also automatically configure the Redux DevTools extension so that you can inspect the store while developing.

# Provide the Redux Store to React

Once the store is created, we can make it available to our React components by putting a React-Redux `<Provider>` around our application in `src/main.jsx`. Import the Redux store we just created, put a `<Provider>` around your `<App>`, and pass the store as a prop:

```jsx
src / main.jsx;

import { StrictMode } from "react";
import { createRoot } from "react-dom/client";
import App from "./App.jsx";
import "./index.css";
import { store } from "./redux/store.js"; //We have to import the store components that we already made in redux.
import { Provider } from "react-redux"; // this is a provider

createRoot(document.getElementById("root")).render(
  <StrictMode>
    <Provider store={store}>
      {" "}
      {/* also wrap the main app in the perovide with given props of store = store this mean we have provided the redux store to our whole app */}
      <App />
    </Provider>
  </StrictMode>
);
// main js is the main component in the react here if we made any changes, the changes will occur in the whole app
```

# Create a Redux State Slice

Add a new file named `src/counter/counterSlice.js`. In that file, import the `createSlice` API from Redux Toolkit.

Creating a slice requires a string name to identify the slice, an initial state value, and one or more reducer functions to define how the state can be updated. Once a slice is created, we can export the generated Redux action creators and the reducer function for the whole slice.

Redux requires that we write all state updates immutably, by making copies of data and updating the copies. However, Redux Toolkit's createSlice and createReducer APIs use Immer inside to allow us to write "mutating" update logic that becomes correct immutable updates.

```jsx
src / counter / counterSlice.js;

import { createSlice } from '@reduxjs/toolkit'
export const counterSlice = createSlice({
  name: 'counter',         // A name for the slice (used for action types).
  initialState: {          // The initial state of the counter.
    value: 0               // The counter starts at 0.
  },
  reducers: {              // Functions (reducers) to change the state.
    increment: (state) => {  // When "increment" is called:
      state.value += 1;      // Add 1 to the current value.
    },
    decrement: (state) => {  // When "decrement" is called:
      state.value -= 1;      // Subtract 1 from the current value.
    },
    incrementByAmount: (state, action) => {  // When "incrementByAmount" is called:
      state.value += action.payload;         // Add a specified amount (from `action.payload`).
    }
  }
});
export const { increment, decrement, incrementByAmount } = counterSlice.actions

export default counterSlice.reducer
```

# Add Slice Reducers to the Store

Next, we need to import the reducer function from the counter slice and add it to our store. By defining a field inside the`reducer` parameter, we tell the store to use this slice reducer function to handle all updates to that state

```jsx
src / redux / store.js;

import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "../counter/counter"; //import This

export default configureStore({
  reducer: {
    counter: counterReducer, // And this (counterReducer is actually counter.reducer)
  },
});
```

# Use Redux State and Actions in React Components

Now we can use the React-Redux hooks to let React components interact with the Redux store. We can read data from the store with `useSelector`, and dispatch actions using `useDispatch`. Create a `src/counter/CounterSlice.js` file with a `<Counter>`component inside, then import that component into `App.js` and render it inside of `<App>`.

```jsx
src / counter / CounterSlice.js;

import React from 'react'
import { useSelector, useDispatch } from 'react-redux'
import { decrement, increment, incrementByAmount } from './counter/counterSlice'
import Navbar from './Com/Navbar'
const App = () => {
  const count = useSelector((state) => state.counter.value)
  const dispatch = useDispatch()
  return (

    <div>
      <Navbar />
      <button onClick={() => dispatch(decrement())} >-</button>
      count is {count}
      <button onClick={() => dispatch(increment())}>+</button>
      <button onClick={() => dispatch(incrementByAmount(10))}>+</button> {/* we use incrementByAmount when we have to change value more than one time in this count will increase +10 when we click */}
    </div>
  )
}

export default App
```
# Using Value of counter in Navbar

```jsx
import React from 'react'
import { useSelector, useDispatch } from 'react-redux' // in order to show the value of the count in components in this case in the navbar we have tp import this.
const Navbar = () => {
  const count = useSelector((state)=>state.counter.value) // this as well
  return (
    <div>
      this is navbar{count}
    </div>
  )
}

export default Navbar
```

# Explination

let's break down the line `const count = useSelector((state) => state.counter.value)` and focus on `state.counter.value`.

### `useSelector` Hook
- `useSelector` is a hook provided by the [`react-redux`](https://redux.js.org/introduction/getting-started) library.
- It allows you to extract data from the Redux store state.
- The function you pass to `useSelector` is called a selector function.

### Selector Function
- The selector function receives the entire Redux state as its argument.
- In this case, the selector function is `(state) => state.counter.value`.

### `state`
- `state` represents the entire Redux store state.
- It is an object that contains all the slices of state defined in your store.

### `state.counter`
- `state.counter` refers to the part of the state managed by the `counter` slice.
- This is because, in your store configuration, you have a reducer named `counter`:
  ```jsx
  export default configureStore({
    reducer: {
      counter: counterReducer,
    },
  });
  ```

### `state.counter.value`
- `state.counter.value` accesses the `value` property of the `counter` slice of the state.
- In your `counterSlice`, the initial state is defined as:
  ```jsx
  initialState: {
    value: 0,
  },
  ```
- So, `state.counter.value` will give you the current value of the counter.

### Putting It All Together
- `const count = useSelector((state) => state.counter.value)` means:
  - Use the `useSelector` hook to get the current state from the Redux store.
  - From the state, access the `counter` slice.
  - From the `counter` slice, get the `value` property.
  - Assign this value to the `count` variable.

Let's clarify the concepts to avoid any confusion.

### Redux State
In [Redux](https://redux.js.org/introduction/getting-started), the **state** is a single JavaScript object that holds the entire state of your application. This state is managed by the Redux store.

### Reducers
Reducers are functions that specify how the state changes in response to actions. Each reducer manages a slice of the state. For example, you might have a `counterReducer` that manages the `counter` slice of the state.

### Store Configuration
When you configure your Redux store, you combine all your reducers into a single root reducer. This root reducer defines the structure of your state object.

Here's an example of how you might configure your store:

```jsx
import { configureStore } from '@reduxjs/toolkit';
import counterReducer from './counterSlice';

const store = configureStore({
  reducer: {
    counter: counterReducer,
  },
});

export default store;
```

In this configuration:
- `counterReducer` is responsible for managing the `counter` slice of the state.
- The `counter` slice is a part of the overall state object.

### Accessing State with `useSelector`
The `useSelector` hook allows you to access the state inside your React components. The function you pass to `useSelector` is called a selector function, which extracts a specific part of the state.

### Example Breakdown
Let's break down the example again:

```jsx
const count = useSelector((state) => state.counter.value);
```

1. **`useSelector` Hook**: This hook is used to access the Redux state.
2. **Selector Function**: `(state) => state.counter.value`
   - **`state`**: This represents the entire Redux state object.
   - **`state.counter`**: This accesses the `counter` slice of the state, which is managed by `counterReducer`.
   - **`state.counter.value`**: This accesses the `value` property within the `counter` slice.

### Putting It All Together
- The Redux state is an object that contains all slices of state.
- Each slice is managed by a corresponding reducer.
- In your store configuration, you named one slice `counter`, managed by `counterReducer`.
- `state.counter` accesses the `counter` slice of the state.
- `state.counter.value` accesses the `value` property within the `counter` slice.

So, `const count = useSelector((state) => state.counter.value)` means:
- Use the `useSelector` hook to get the current state from the Redux store.
- From the state, access the `counter` slice.
- From the `counter` slice, get the `value` property.
- Assign this value to the `count` variable.

Yes, exactly! The **`payload`** will be the number (or any other data) that you **pass** when you dispatch the action.

For example:

```js
dispatch(incrementByAmount(10));
```

Here:
- The `payload` is `10`, because that's the number you're passing when calling `incrementByAmount(10)`.

In the reducer:
```js
incrementByAmount: (state, action) => {
  state.value += action.payload;
}
```

- `action.payload` will hold the value `10`, which gets added to `state.value`.

So, **`payload`** is just the data you're sending with the action, and it can be any type of value (like numbers, strings, or even objects), depending on what your action needs.

Exactly! 🎯

With **Redux**, you don't need to manually pass the state as **props** between components like you would in traditional React. Instead, you can simply use the **`useSelector`** hook to access the **global state** directly in any component that needs it.

Here's the difference:

### Without Redux (Using Props):
You need to pass the `count` as a prop from the parent to child components:
```jsx
const Navbar = ({ count }) => {
  return <div>This is Navbar, counter value: {count}</div>;
};

// In the parent component
<Navbar count={count} />
```
This approach requires **prop drilling**—passing `count` through the parent, which can get messy as the app grows.

---

### With Redux (Using `useSelector`):
You no longer need to pass the `count` as a prop. Instead, **any component** can just access the `count` value directly from the Redux store using `useSelector`:

```jsx
const Navbar = () => {
  const count = useSelector((state) => state.counter.value); // Directly access Redux state
  return <div>This is Navbar, counter value: {count}</div>;
};
```

### **Key Benefits:**
1. **No Prop Drilling**: You don't have to pass `count` from a parent component. Each component can independently access the state from the Redux store.
2. **Centralized State**: All components use the same global state, so the `count` is consistent across the app.
3. **Easier to Manage**: As your app grows, Redux makes it easier to manage state shared across multiple components without passing props.

So, in Redux, instead of passing data through props, each component can directly "select" the part of the global state it needs using `useSelector`, making the code much simpler and scalable.

Yes, you’re absolutely right! 🎯

### How It Works:
- **`useSelector`** allows your component to access specific pieces of the **global Redux state**.
- In your example, you used `state.counter.value` to access the `value` property within the `counter` slice of the state.

### Breakdown:
- **`state`**: Represents the entire Redux store, which contains all the state for your application.
- **`state.counter`**: Refers to the `counter` slice of that state. This slice contains everything related to the counter feature, including the `value`.
- **`state.counter.value`**: This specifically gets the `value` property from the `counter` slice, which holds the current count you want to display.

### Example Context:
So when you write:
```js
const count = useSelector((state) => state.counter.value);
```
- You are telling your component: “I want to access the current value of the counter from the global state.” 

### Summary:
- **Yes**, you’re accessing a specific piece of state that you need for your component.
- By using `useSelector`, you can pull in only the data necessary for that component, making it efficient and clean.

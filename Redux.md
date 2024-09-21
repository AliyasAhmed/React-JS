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

import { createSlice } from "@reduxjs/toolkit";

export const counterSlice = createSlice({
  name: "counter",
  initialState: {
    value: 0,
  },
  reducers: {
    increment: (state) => {
      // Redux Toolkit allows us to write "mutating" logic in reducers. It
      // doesn't actually mutate the state because it uses the Immer library,
      // which detects changes to a "draft state" and produces a brand new
      // immutable state based off those changes
      state.value += 1;
      // We know in react we have to use usestate in order to increament something but in redux state.value += 1 is what we use instead
    },
    decrement: (state) => {
      state.value -= 1;
      // as usual it will decrement means will reduce the numbers
    },
    incrementByAmount: (state, action) => {
      state.value += action.payload;
    },
  },
});

// Action creators are generated for each case reducer function
export const { increment, decrement, incrementByAmount } = counterSlice.actions;

export default counterSlice.reducer;
```

# Add Slice Reducers to the Store

Next, we need to import the reducer function from the counter slice and add it to our store. By defining a field inside the`reducer` parameter, we tell the store to use this slice reducer function to handle all updates to that state

```jsx
src / redux / store.js;
import { configureStore } from "@reduxjs/toolkit";
import counterReducer from "../features/counter/counterSlice"; //import This

export default configureStore({
  reducer: {
    counter: counterReducer, // And this
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

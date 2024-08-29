# **What is `useRef`?**

### When `state` is changed this will re-render but due to re-render the value of a will set back to `0`. But If we use `useRef` out value wont be rendered and will be updated.

### Example Without UseRef
  ```jsx
  // Without UseRef Example
  
  import React from "react";
  import { useState, useRef, useEffect } from "react";
  const App = () => {
    const [count, Setcount] = useState(0);
    // as we already know our app re-renders whenever a state is changed we can see that with the help of useEffect
    let a = 0
    useEffect(() => { 
      a = a + 1;
      console.log(`rendering and the value of a is ${a}`) //When state is changed this will re-render
      //but due to re-render the value of a will set back to 0. But If we use useRef out value wont be rendered and will be 
      //updated
    });
    return (
      <div>
        <p>Count {count}</p>
        <button onClick={() => Setcount(count + 1)}>Click</button>
      </div>
    );
  };
  
  export default App;
  ```
### Example With UseRef
  ```jsx
  // Without UseRef Example

import React from "react";
import { useState, useRef, useEffect } from "react";
const App = () => {
  const [count, Setcount] = useState(0);
  // as we already know our app re-renders whenever a state is changed we can see that with the help of useEffect

  // let a = 0 instead of this we use
  const a = useRef(0) // this will save the value and everythime the app re-renders it will remain same and let the update do it thing.
  useEffect(() => { 
    a.current = a.current + 1; // but we have to use a.current 
    console.log(`rendering and the value of a is ${a.current}`) //When state is changed this will re-render
  //but due to re-render the value of a will set back to 0. But If we use useRef out value wont be rendered and will be updated
  });
  return (
    <div>
      <p>Count {count}</p>
      <button onClick={() => Setcount(count + 1)}>Click</button>
    </div>
  );
};

export default App;
```
### State Changes and Re-renders:

When you change state in a React component (e.g., using `useState`), the component re-renders, and the updated state value is reflected in the rendered output. However, if you have other variables or values in the component that are not part of the state, they will be reset to their initial values on each re-render unless they are managed differently.

### Using `useRef`:

`useRef` is a hook that can be used to keep a value that doesn’t cause a re-render when it changes. It allows you to store a value that persists across renders without triggering a component update. This is useful for keeping track of values like timers or previous state values.

`useRef` is a React hook that lets you create a reference to a DOM element or store a value that you can change without making your component re-render.

### **Why Do We Use `useRef`?**

1. **To Access DOM Elements**: You can use `useRef` to grab and interact with elements like input fields directly.
2. **To Store a Value**: You can store a value that needs to stay the same even after the component updates, but you don't want the component to re-render when that value changes.

### **Simple Example**

  ```javascript
  import React, { useRef } from 'react';
  
  function FocusInput() {
    const inputRef = useRef(null);
  
    const handleClick = () => {
      inputRef.current.focus(); // Focus the input when the button is clicked
    };
  
    return (
      <div>
        <input ref={inputRef} type="text" />
        <button onClick={handleClick}>Focus the Input</button>
      </div>
    );
  }
  
  export default FocusInput;
  ```

# Use of UserRef With Example
  ```javascript
  import { useState, useEffect, useRef } from 'react'
  import reactLogo from './assets/react.svg'
  import viteLogo from '/vite.svg'
  import './App.css'
  
  function App() {
    const [count, setCount] = useState(0)
    const a = useRef(0)
  
    useEffect(() => {
      a.current = a.current + 1
      console.log(`rerendering and the value of a is ${a.current}..`) 
    });
    
  
    return (
      <>
        <div>
          <a href="https://vitejs.dev" target="_blank">
            <img src={viteLogo} className="logo" alt="Vite logo" />
          </a>
          <a href="https://react.dev" target="_blank">
            <img src={reactLogo} className="logo react" alt="React logo" />
          </a>
        </div>
        <h1>Vite + React</h1>
        <div className="card">
          <button onClick={() => setCount((count) => count + 1)}>
            count is {count}
          </button>
          <p>
            Edit <code>src/App.jsx</code> and save to test HMR
          </p>
        </div>
        <p className="read-the-docs">
          Click on the Vite and React logos to learn more
        </p>
      </>
    )
  }
  
  export default App
  ```
- **Explanation**: 
  - **`useRef(null)`** creates a reference to the input element.
  - When you click the button, it focuses on the input field without causing the component to re-render.

This way, `useRef` is a handy tool for directly interacting with elements or storing values that don't need to trigger re-renders.

If we don't use `useref` here and initialize the value to '0', every time we click on the button, it will be `1` and then zero again. The value won't be saved in memory.
But with 'useref', whenever the code re-renders, the value will be increased.

# Use of useRef In manipulating dom

  ```javascript 
  import { useState, useEffect, useRef } from 'react'
  import reactLogo from './assets/react.svg'
  import viteLogo from '/vite.svg'
  import './App.css'
  
  function App() {
    const [count, setCount] = useState(0)
    const a = useRef(0)
    const btnref = useRef()
    useEffect(()=>{
      a.current = a.current + 1
      btnref.current.style.backgroundColor = "aqua"
      btnref.current.style.color = "black"
      console.log(`value of a is ${a.current}`)
  
    })
  
    return (
      <>
        <div>
          <a href="https://vitejs.dev" target="_blank">
            <img src={viteLogo} className="logo" alt="Vite logo" />
          </a>
          <a href="https://react.dev" target="_blank">
            <img src={reactLogo} className="logo react" alt="React logo" />
          </a>
        </div>
        <h1>Vite + React</h1>
        <div className="card">
          <button ref={btnref} onClick={() => setCount((count) => count + 1)}>
            count is {count}
          </button>
          <p>
            Edit <code>src/App.jsx</code> and save to test HMR
          </p>
        </div>
        <p className="read-the-docs">
          Click on the Vite and React logos to learn more
        </p>
      </>
    )
  }
  
  export default App
    
  ```

### **Explanation of `useRef` in Your New Example**

In this code, `useRef` is used to reference the `<button>` element so you can interact with it directly in JavaScript.

### **What is `useRef` Doing Here?**

- **Initialization**: 
  ```javascript
  const btnRef = useRef();
  ```
  - `btnRef` is a reference object created using `useRef()`. Initially, `btnRef.current` is `undefined`, but after the first render, it will point to the button element in the DOM.

- **Accessing the Button in `useEffect`**:
  ```javascript
  useEffect(() => { 
    console.log(`First rendering..`); 
    btnRef.current.style.backgroundColor = "red";
  }, []);
  ```
  - This `useEffect` runs only once after the initial render (because of the empty dependency array `[]`).
  - Inside `useEffect`, `btnRef.current` is used to change the button's background color to red. This directly modifies the DOM element referenced by `btnRef`.

- **Interacting with the Button on Click**:
  ```javascript
  <button onClick={() => { btnRef.current.style.display = "none"; }}>
    Change me
  </button>
  ```
  - This second button uses `btnRef.current` to hide the first button when clicked. It directly manipulates the `display` style of the referenced button, making it disappear from the screen.

### **Key Points:**

- **`useRef`** allows you to get a direct reference to the DOM element (`<button>`) so you can manipulate it in JavaScript without causing re-renders.
- In this code:
  - **`btnRef.current.style.backgroundColor = "red"`** changes the button's background color after the first render.
  - **`btnRef.current.style.display = "none"`** hides the button when the "Change me" button is clicked.

### **Why Use `useRef` Here?**

- **Direct DOM Manipulation**: `useRef` is perfect for cases where you need to directly interact with a DOM element, such as changing its style or visibility, without triggering a re-render of the component. 
- **Performance**: Since `useRef` doesn't cause re-renders, it's more efficient for tasks like changing styles or other direct DOM manipulations.

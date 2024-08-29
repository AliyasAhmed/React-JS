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

- **Explanation**: 
  - **`useRef(null)`** creates a reference to the input element.
  - When you click the button, it focuses on the input field without causing the component to re-render.

This way, `useRef` is a handy tool for directly interacting with elements or storing values that don't need to trigger re-renders.

If we don't use `useref` here and initialize the value to '0', every time we click on the button, it will be `1` and then zero again. The value won't be saved in memory.
But with 'useref', whenever the code re-renders, the value will be increased.

## Diffrence Between `useRef` and `useState`.

Both `useRef` and `useState` are useful for different purposes, and choosing between them depends on what you need to do in your component.

### Differences Between `useState` and `useRef`

1. **Triggering Re-renders:**
   - **`useState`:** Changing a state value with `useState` triggers a re-render of the component. This is useful when you want the UI to update in response to state changes.
   - **`useRef`:** Changing the `.current` property of a `useRef` object does not trigger a re-render. This is useful for storing values that you don’t want to directly affect the UI.

2. **When to Use `useState`:**
   - Use `useState` when you need to update the UI based on changes. For example, if you have a counter that needs to be displayed and updated, you should use `useState` because you want the component to re-render and show the new count.

3. **When to Use `useRef`:**
   - Use `useRef` when you need to persist values across renders without causing re-renders. This is useful for storing mutable values, like timers, DOM references, or any value that should not directly affect the UI.


### Summary:

- **Use `useState`** when you need to track and display state changes in the UI.
- **Use `useRef`** for values that need to persist across renders but shouldn’t cause re-renders when updated.

Both hooks are powerful, and choosing the right one depends on whether you need to affect the component's render behavior.

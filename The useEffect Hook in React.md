```
The command `code -r filename` is used to open a file in Visual Studio Code and closing the previous files. Here's what each part does:

- `code`: This is the command to open Visual Studio Code from the terminal.
- `-r`: This stands for "reuse window." It opens the file in an already open Visual Studio Code window, instead of opening a new one.
- `dirname`: This is the name of the file you want to open.

So, `code -r dirname` will open the specified file in the current Visual Studio Code window. In short we dont have to do `cd` to specific folder again and again all we can do is `code -r dirname`
```
# The useEffect Hook in React

The useEffect Hook allows you to perform side effects in your components. Some examples of side effects are: fetching data, directly updating the DOM, and timers. useEffect accepts two arguments. The second argument is optional.
useEffect`(<function>, <dependency>)`

# Basic Structure of useEffect
  ```javascript
  import React, { useEffect } from 'react';
  
  function MyComponent() {
    useEffect(() => {
      // Code to run on component mount/update
  
      return () => {
        // Code to run on component unmount (cleanup)
      };
    }, []); // Dependency array
  }
  ```

### Basic Example of UseEffect
  ```javascript
  import React, { useEffect, useState } from 'react'
  import './App.css';
  function App() {
    const [count, setcount] = useState(0)
    useEffect(() => {
      alert('this is my first use effect')
    }, []);
    return (
      <div>
        <h1>{count}</h1>
        <button onClick={()=>setcount(count+1)}>Click me</button>
      </div>
    )
  }
  
  export default App
  ```

### Use setTimeout() to count 1 second after initial render:

  ```javascript
  import { useState, useEffect } from "react";
  import ReactDOM from "react-dom/client";
  
  function Timer() {
    const [count, setCount] = useState(0);
  
    useEffect(() => {
      setTimeout(() => {
        setCount((count) => count + 1);
      }, 1000);
    });
  
    return <h1>I've rendered {count} times!</h1>;
  }
  
  const root = ReactDOM.createRoot(document.getElementById('root'));
  root.render(<Timer />);
  ```

But wait!! It keeps counting even though it should only count once!
`useEffect` runs on every render. That means that when the count changes, a render happens, which then triggers another effect.
This is not what we want. There are several ways to control when side effects run.
We should always include the second parameter which accepts an array. We can optionally pass dependencies to `useEffect` in this array.

### Example
1. No dependency passed:
  ```javascript
  useEffect(() => {
    //Runs on every render
  });
  ```

`useEffect` in React is versatile and can be used for various purposes beyond just running code on mount. Here are some common scenarios where `useEffect` is helpful:

### 1. **Fetching Data**
```javascript
useEffect(() => {
  fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => {
      // Process fetched data
    });
}, []);
```
# - Uses of `useEffect` 

### 2. **Subscriptions and Event Listeners**
```javascript
useEffect(() => {
  const subscription = someService.subscribe(handleDataChange);
  return () => {
    subscription.unsubscribe();
  };
}, []);
```
- Use `useEffect` to set up subscriptions or event listeners and clean them up when the component unmounts.

### 3. **Updating the DOM**
```javascript
useEffect(() => {
  document.title = `You clicked ${count} times`;
}, [count]);
```
- Use `useEffect` to update parts of the DOM directly, like setting the document title based on state changes.

### 4. **Integration with Libraries or External APIs**
```javascript
useEffect(() => {
  const script = document.createElement('script');
  script.src = 'https://example.com/library.js';
  script.async = true;
  document.body.appendChild(script);
  return () => {
    document.body.removeChild(script);
  };
}, []);
```
- Use `useEffect` to integrate with third-party libraries or load scripts dynamically.

### 5. **Performing Cleanup**
```javascript
useEffect(() => {
  const timer = setInterval(() => {
    // Do something periodically
  }, 1000);
  return () => {
    clearInterval(timer);
  };
}, []);
```
- Use `useEffect` to set up cleanup operations, like clearing intervals or timeouts.

### 6. **Conditional Effects**
```javascript
useEffect(() => {
  if (someCondition) {
    // Perform effect when condition is true
  }
}, [someCondition]);
```
- Use `useEffect` with dependencies to conditionally run code based on state or props changes.

### 7. **Optimizing Performance**
```javascript
useEffect(() => {
  // Expensive calculations or operations
  return () => {
    // Cleanup or cancel operations
  };
}, [dependency]);
```
- Use `useEffect` to optimize performance by running effects only when necessary, controlled by the dependency array.

### Summary:
`useEffect` is a powerful tool in React for managing side effects in function components. It provides a way to perform actions that need to happen in response to component lifecycle events, state changes, or external interactions, ensuring your components are dynamic and responsive to data and user actions.

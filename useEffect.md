# The useEffect Hook in React

`useEffect` is a hook in React that lets you run some code whenever your component is added to the page, updated, or removed. Think of it as a way to tell React, "Hey, when this component shows up, do this," or "Before this component goes away, clean up this." For example, you might use it to fetch data when the component loads or to set up a timer that stops when the component is no longer needed. The `useEffect` hook runs the code based on the changes in the data or variables you specify, so you can control exactly when and how often it happens.

The useEffect Hook allows you to perform side effects in your components. Some examples of side effects are: fetching data, directly updating the DOM, and timers. useEffect accepts two arguments. The second argument is optional.
useEffect`(<function>, <dependency>)`


# Basic Structure of useEffect
  ```javascript
    import React, { useEffect } from 'react';
    
    function MyComponent() {
      useEffect(() => {
        // This runs when the component is first added to the page or when it updates
    
        return () => {
          // This runs when the component is removed from the page (cleanup)
        };
      }, []); // Dependency array: an empty array means this only runs once when the component is first added
    }

  ```

1. **`useEffect` Behavior:** In React, `useEffect` does run after every render if it has dependencies listed in its dependency array. If you include state variables in the dependency array, the effect will run whenever those state variables change. If the dependency array is empty (`[]`), the effect runs only once, after the initial render.

2. **Effect and Re-renders:** It’s important to note that `useEffect` itself doesn’t cause re-renders. Re-renders are triggered by state changes or prop updates. If an effect inside `useEffect` causes state updates, that will trigger another render.

3. **Alerts in `useEffect`:** If you have an `alert` inside `useEffect`, it will be triggered based on how you configure the dependency array. If `count` is a dependency, the alert will show up every time `count` changes, which may not always be desirable.

Here’s a refined summary:
- **State Changes:** When state changes (e.g., `count`), the component re-renders to reflect the updated state.
- **`useEffect` Execution:** The `useEffect` hook runs after every render based on its dependencies. If `count` is included in the dependency array, `useEffect` will run after every change to `count`.
- **Alerts in `useEffect`:** An `alert` inside `useEffect` will show up according to the dependencies. If the dependency array includes a state variable like `count`, the alert will appear each time that state changes.


### Basic Example of UseEffect
  ```javascript
  import React, { useEffect, useState } from 'react'
  import './App.css';
  function App() {
    const [count, setcount] = useState(0)
    useEffect(() => {
      alert('Count was changed')
    }, [count]);
    return (
      <div>
        <h1>{count}</h1>
        <button onClick={()=>setcount(count+1)}>Click me</button>
      </div>
    )
  }
  
  export default App
  ```

This will trigger whenever we click on count and it changes the value. Remember we used the count in the array [] section to tell the useEffect 'hey whenever you see count value is changed show an alert.'

Let's look at a simple example comparing how you would do something in plain JavaScript (JS) versus how you'd achieve the same thing in JSX (React).

### Scenario: Displaying a Message on Page Load

**JavaScript Approach:**
In plain JavaScript, you might use the `window.onload` event to run some code when the page loads. Here's how you would display a message:

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>JavaScript Example</title>
  <script>
    // JavaScript function to run when the page loads
    window.onload = function() {
      alert('Welcome to the page!');
    };
  </script>
</head>
<body>
  <h1>Hello World</h1>
</body>
</html>
```

**JSX (React) Approach:**
In React, you would use the `useEffect` hook to run code when the component is first added to the page. Here’s how the same example would look in JSX:

```jsx
import React, { useEffect } from 'react';

function WelcomeComponent() {
  // Using useEffect to run code when the component is added
  useEffect(() => {
    alert('Welcome to the page!');
  }, []); // Empty dependency array means it runs only once

  return (
    <div>
      <h1>Hello World</h1>
    </div>
  );
}

export default WelcomeComponent;
```

### Explanation:

- **JavaScript (`window.onload`)**:
  - Runs the function when the entire page (HTML, CSS, JS) has finished loading.
  - It’s suitable for simple, static websites or basic scripts.

- **JSX (`useEffect`)**:
  - `useEffect` is more flexible and designed for React’s component-based structure.
  - Runs the function when the React component is mounted (first displayed) or when dependencies change.
  - Works better for dynamic, interactive user interfaces, like those created with React.

So, in simple terms, both approaches are doing something when the page or component loads, but React’s `useEffect` offers more control over when and how this happens, making it more suitable for modern web apps.

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

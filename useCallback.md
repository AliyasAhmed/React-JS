##  `useCallback` in Simple Words

The React `useCallback` Hook returns a memoized callback function.

Think of memoization as caching a value so that it does not need to be recalculated.

This allows us to isolate resource intensive functions so that they will not automatically run on every render.

The `useCallback` Hook only runs when one of its dependencies update.

This can improve performance.

The `useCallback` and `useMemo` Hooks are similar. The main difference is that `useMemo` returns a memoized value and `useCallback` returns a memoized function.

## Problem

One reason to use useCallback is to prevent a component from re-rendering unless its props have changed.


`useCallback` is a React Hook that helps you **remember a function**. When you create a function inside a component, it gets recreated every time the component re-renders. Sometimes, this can cause performance issues, especially if you are passing the function to child components. `useCallback` prevents this by **"remembering"** the same function so that it doesn't change unless its dependencies change.

In simpler terms:
- **Without `useCallback`**: A new function is created every time the component updates.
- **With `useCallback`**: The same function is reused unless something it depends on changes.

### Basic Syntax of `useCallback`

```jsx
const memoizedFunction = useCallback(() => {
  // Function logic here
}, [dependencies]);
```

- `memoizedFunction` is the function that you want to "remember."
- The **dependency array** (`[dependencies]`) tells React when to recreate the function. If the dependencies don’t change, the function remains the same.

### Basic Example of `useCallback`


### Summary

`useCallback` is helpful when you want to **prevent unnecessary re-creations** of a function, especially when passing it to optimized child components that don't need to re-render unless necessary. This can help improve the performance of your React app.

### Key Points:

1. **`useRef` is not for functions:** `useRef` is mainly used for storing mutable values or accessing DOM elements. When you use `useRef` to store a value (like a DOM reference or a variable), updating the `.current` property does not cause a re-render. However, `useRef` is not designed to prevent the re-creation of functions on every render.

2. **`useCallback` is for memoizing functions:** When you have a function that you don't want to be recreated on every re-render of a component, you use `useCallback`. This is particularly important when you are passing that function to a child component. If the child component is wrapped in `React.memo` (which prevents re-renders when props don't change), a newly created function will make the child component re-render unnecessarily. `useCallback` provides the same function reference between renders if the dependencies don’t change.

### Example to Understand the Difference:

Let's say you have a parent component that passes a function as a prop to a child component. If you don't use `useCallback`, a new function is created on every render, causing the child component to re-render even if nothing else has changed.

#### Without `useCallback`:

```jsx
import React, { useState } from 'react';

const ChildComponent = React.memo(({ handleClick }) => {
  console.log('ChildComponent re-rendered');
  return <button onClick={handleClick}>Click Me</button>;
});

const ParentComponent = () => {
  const [count, setCount] = useState(0);

  // Function is recreated on every render
  const handleClick = () => {
    console.log('Button clicked!');
  };

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <ChildComponent handleClick={handleClick} />
    </div>
  );
};

export default ParentComponent;
```

- In this example, the `ChildComponent` will re-render every time the `ParentComponent` renders because a new `handleClick` function is created on each render.

#### With `useCallback`:

```jsx
import React, { useState, useCallback } from 'react';

const ChildComponent = React.memo(({ handleClick }) => {
  console.log('ChildComponent re-rendered');
  return <button onClick={handleClick}>Click Me</button>;
});

const ParentComponent = () => {
  const [count, setCount] = useState(0);

  // Function is memoized and does not get recreated on each render
  const handleClick = useCallback(() => {
    console.log('Button clicked!');
  }, []); // No dependencies, so it stays the same

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
      <ChildComponent handleClick={handleClick} />
    </div>
  );
};

export default ParentComponent;
```

- Now, `handleClick` is memoized, and it doesn’t change between renders. Therefore, `ChildComponent` will not re-render unless its props change.

### Summary:
- **`useRef`**: Not suitable for functions; it doesn’t help prevent a function from being recreated on each render.
- **`useCallback`**: Specifically designed to memoize functions, ensuring the function reference remains the same between renders unless its dependencies change.

Using `useCallback` effectively helps in optimizing component rendering and improving performance in React applications.

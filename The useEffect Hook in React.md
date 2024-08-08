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

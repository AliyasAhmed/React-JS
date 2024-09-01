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

## Clear Definition

Steps to Follow,
1. Make a chid component name it anything in my case i named it as Navbar.
2. in navbar make anyfunction in my case i started with the simple case as console.log('this is the child component)
3. next we pass the child component in the main app and when we start out app on browser we'll see that the when the state is changing on count, because out button component is a state the the child will be re-rendered which we dont want because if the child component had any complicated function it would create a big problem for the app. 
4. In order to solve the problem we use memo for now, we can import memo from react and use it like this 'export default memo(Navbar)'. This way our child component will be memorized. But this is only when we dont have any props in the child component.

5. If we have props in the child component.
6. First we make a function which we named as prop and passed it in the child component like this '<Navbar prop={prop}/>'. and in the child component we have to call it as well like this 'const Navbar = (prop) =>' so now our problem will start to rise again. For that we use 'usecallback'.

7. instead of this 'const prop = ()=>', we call callback like this 'const prop = useCallback(()=>' and then we also make an emty array so our child component renders only once.

8. Next lets add another prop as state which we want to update and re-renders only if we want to, so we make it and name it as add and aslo pass it in the child component like this '<Navbar prop={prop} add={add} />' and int the other page of the child component navbar. and make a button which we the add changes the child component will re-render but if we click on count the child component will not re-render.


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
### Child Component
  ```jsx
  import {React, memo} from 'react'
  
  const Navbar = (prop, add) => {
      console.log('child component from navbar') // this is the child componet which we are using in the main app component, also we are using usestate and when the state changes this console will will re-render and make the app slow and wont be optimized thats the reasone we use use call back. For now if we use memo in this component it will solve out problem.
    return (
      <div>
        
      </div>
    )
  }
  
  export default memo(Navbar) // we need to use the memo function which is going to memorize the function and wont let it re-render the child component.
  //but for now our problem is solved. But if we use any props for our child it will start to re-render again because child will think this is part of state.
  // we have passed the prop from main app and if we use console.log in the chrome browser we will see the problem will rise again an the re-render will start again.
  // for that problem we use UseCallBack().
  ```

### Main App Component

  ```jsx
  import React, { useCallback, useState } from 'react'
  import Navbar from './Com/Navbar'
  const App = () => {
    const [count, setcount] = useState(0)
    const [add, setadd] = useState(0)
    // const prop = ()=> { //with this prop function that we passed in the child component out child will start to re-render again. for that we use usecallback.
    //   console.log('this is prop')
    // }
    const prop = useCallback(() => {
      console.log('this is prop') //but in order for it to work we need to use an emty array so it will render only once, as we also saw in useEffect
    }, [add])
    return (
      <div>
        <Navbar prop={prop} add={add} />
        <p>count {count}</p>
        <button onClick={() => setcount(count + 1)}>count</button>
        <button onClick={()=>setadd(add+1)}>add</button>
      </div>
    )
  }
  
  export default App
  ```
### Summary:
- **`useRef`**: Not suitable for functions; it doesn’t help prevent a function from being recreated on each render.
- **`useCallback`**: Specifically designed to memoize functions, ensuring the function reference remains the same between renders unless its dependencies change.

Using `useCallback` effectively helps in optimizing component rendering and improving performance in React applications.

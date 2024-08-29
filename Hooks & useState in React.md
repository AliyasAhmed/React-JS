# State Hooks 
State lets a component “remember” information like user input. For example, a form component can use state to store the input value, while an image gallery component can use state to store the selected image index.
The `useState` hook in React is a handy tool for managing and updating state in your components. When you call `useState`, you create a state variable with an initial value and get a function to change that value. For example, if you use `const [count, setCount] = useState(0)`, you start with `count` set to `0`, and `setCount` is the function you use to update `count` whenever needed. It’s like having a variable in your component that can change over time, and React takes care of keeping everything updated and in sync with the UI.
To add state to a component, use one of these Hooks:


# **`useState`**


1. **Basic Counter Example**

   ```javascript
   import React, { useState } from 'react';

   function Counter() {
     // Declare a state variable called "count" with an initial value of 0
     const [count, setCount] = useState(0);

     return (
       <div>
         <p>Count: {count}</p>
         <button onClick={() => setCount(count + 1)}>Increase</button>
         <button onClick={() => setCount(count - 1)}>Decrease</button>
       </div>
     );
   }

   export default Counter;
   ```
   `const [count, setcount] = useState(0)`
   
it means make a `count` which has initial value `0` and make `setcount` which helps us `update` the initial value



In React, when a state changes, the entire component re-renders to reflect the updated state. For example, if you have a `count` state managed with `useState`, changing the value of `count` will cause the component to re-render, and you’ll see the updated `count + 1`.

If you use `useEffect` inside this component, any side effects (like an `alert` message) will run on every re-render, depending on the dependencies you specify in `useEffect`. If the dependency array is empty (`[]`), the effect runs only once after the initial render. However, if the dependency array includes state variables like `count`, the effect will run after every state change, causing the `alert` to show up repeatedly with each update.



This clarifies the behavior of `useEffect` and `useState` in the context of component re-renders and side effects.
   ```jsx
         // React useContext() hook introduction 🧑‍💻
      
      import React, { useState } from 'react';
      import ComponentB from './ComponentB.jsx';
      
      function ComponentA() {
        const [user, setUser] = useState("BroCode"); // with the help of `setuser` we can set variables anytime in the code where as with `user` we already defined the variable as `brocode`.
      
        return (
          <div className="box">
            <h1>ComponentA</h1>
            <h2> Hello ${user}</h2>
            <ComponentB />
          </div>
        );
      }
      
      export default ComponentA;
      ```
   - **`useState(0)`** initializes the state with `0`.
   - **`count`** is the current state value.
   - **`setCount`** updates the state when the button is clicked.
   - Clicking the "Increase" button adds 1 to the count, and "Decrease" subtracts 1.


These examples illustrate how `useState` and `useEffect` can be used to manage state and side effects in functional components in a simple and effective way.




# **State with `useState`**

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

   - **`useState(0)`** initializes the state with `0`.
   - **`count`** is the current state value.
   - **`setCount`** updates the state when the button is clicked.
   - Clicking the "Increase" button adds 1 to the count, and "Decrease" subtracts 1.

### **Effect with `useEffect`**

2. **Fetching Data Example**

   ```javascript
   import React, { useState, useEffect } from 'react';

   function DataFetcher() {
     const [data, setData] = useState(null);

     useEffect(() => {
       // Fetch data when the component mounts
       fetch('https://api.example.com/data')
         .then(response => response.json())
         .then(data => setData(data))
         .catch(error => console.error('Error fetching data:', error));
     }, []); // Empty array means this effect runs only once, when the component mounts

     return (
       <div>
         <h1>Data:</h1>
         {data ? (
           <pre>{JSON.stringify(data, null, 2)}</pre>
         ) : (
           <p>Loading...</p>
         )}
       </div>
     );
   }

   export default DataFetcher;
   ```

   - **`useEffect`** is used to perform side effects, such as data fetching.
   - The effect runs once when the component mounts (because of the empty dependency array `[]`).
   - When data is fetched, it is stored in the `data` state, and the component re-renders to display it.

### **Combining State and Effect**

3. **Example with State

   ```javascript
    import React, { useState } from 'react';
    
    function Counter() {
      // Declare a state variable called "count" with an initial value of 0
      const [count, setCount] = useState(0);
    
      // Function to handle button click and increase the count
      const handleClick = () => {
        setCount(count + 1);
      };
    
      return (
        <div>
          <p>Count: {count}</p>
          <button onClick={handleClick}>Increase Count</button>
        </div>
      );
    }
    
    export default Counter;

   ```

   - **State**: `inputValue` keeps track of the input field value. `submittedValue` stores the value after form submission.

These examples illustrate how `useState` and `useEffect` can be used to manage state and side effects in functional components in a simple and effective way.

# State Hooks 
State lets a component “remember” information like user input. For example, a form component can use state to store the input value, while an image gallery component can use state to store the selected image index.

To add state to a component, use one of these Hooks:

useState declares a state variable that you can update directly.
useReducer declares a state variable with the update logic inside a reducer function.
  ```javascript
  function ImageGallery() {
    const [index, setIndex] = useState(0);
  ```

# Context Hooks 
Context lets a component receive information from distant parents without passing it as props. For example, your app’s top-level component can pass the current UI theme to all components below, no matter how deep.
  ```javascript
  useContext reads and subscribes to a context.
  function Button() {
    const theme = useContext(ThemeContext);
  ```

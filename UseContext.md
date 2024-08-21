### `useContext` Hook Explanation Using Your Examples
#### Rules to Follow
      ```
      // useContext() = React Hook that allows you to share values
      //                between multiple levels of components
      //                without passing props through each level
      
      // PROVIDER COMPONENT
      // 1. import {createContext} from 'react';
      // 2. export const MyContext = createContext();
      // 3. <MyContext.Provider value={value}>
      //      <Child />
      //    </MyContext.Provider>
      
      // CONSUMER COMPONENTS
      // 1. import React, { useContext } from 'react';
      // 2. import { MyContext } from './ComponentA';
      // 3. const value = useContext(MyContext);
      
      import ComponentA from './ComponentA.jsx';
      import React from 'react';
      
      function App() {
        return(<ComponentA />);
      }
      
      export default App;
      ```
**What is `useContext`?**

The `useContext` hook in React is used to access the value provided by a context. Context is a way to pass data through the component tree without having to pass props down manually at every level.
In short we can use it again and again in every jsx file without using props to call it. we just need to make one file with createcontext then export it.

### Step-by-Step Explanation
### First we need to make a folder with anyname and make a `js` file in which we do this =>
1. **Creating a Context:**
   ```javascript
   import { createContext } from "react";
   export const CounterContent = createContext(0);
   ```

   - Here, you create a context called `CounterContent` using `createContext`.
   - The initial value of this context is `0`.

2. **Providing Context Value:**
   ```javascript
      import React, { useState } from 'react'
      import { CounterContent } from './content/content'
      import Navbar from './components/navbar'
      
      const App = () => {
        const [count, setcount] = useState(0)
        return (
          <>
          {/* if we wrap our context in a <CounterContent.Provider> every context within will have the same context we need */}
          <CounterContent.Provider value={{count, setcount}}> 
          <Navbar/>
          <div>
            <button onClick={()=>setcount((count)=>count+1)}>
              count is {count}
            </button>
          </div>
          </CounterContent.Provider>
          </>
        )
      }
      
      export default App

   ```

   - In the `App` component, the `CounterContent.Provider` wraps around the components (`Navbar` and the button).
   - This `Provider` makes the `count` and `setcount` values available to any component inside it.

3. **Consuming the Context Value in `Button`:**
   ```javascript
   import React, { useContext } from 'react';
   import { CounterContent } from '../content/content';

   const Button = () => {
     const value = useContext(CounterContent);

     return (
       <div>
         <button onClick={() => value.setcount((count) => count + 1)}>
           count is {value.count}
         </button>
       </div>
     );
   };

   export default Button;
   ```

   - In the `Button` component, `useContext(CounterContent)` is used to access the context value.
   - `value.count` and `value.setcount` are accessed from `CounterContent`.
   - When the button is clicked, it updates the `count` value, which is shared across all components that consume this context.

4. **Using Context in `components1`:**
   ```javascript
   import React, { useContext } from 'react';
   import { CounterContent } from '../content/content';

   const components1 = () => {
     const counter = useContext(CounterContent);

     return (
       <div>
         {counter.count}
       </div>
     );
   };

   export default components1;
   ```

   - In `components1`, `useContext(CounterContent)` is again used to access the shared context.
   - Here, `counter.count` is displayed, which will update whenever the `count` state in `App` changes.

### How It Works:
- The `count` state is managed in the `App` component.
- This state and its updater function are shared with the `Navbar`, `Button`, and `components1` components via the `CounterContent` context.
- Any change in the `count` value in one of these components will reflect in others because they all consume the same context.

### Why Use `useContext`?
- It simplifies state management when you have to pass data through many layers of components.
- Instead of prop drilling (passing props through multiple components), you can directly access the data wherever it's needed.

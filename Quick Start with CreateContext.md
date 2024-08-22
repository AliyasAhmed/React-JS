### Quick Start with `useContext`

The `useContext` hook in React is used to consume context values without the need to pass props down through every level of the component tree. Here's a quick start guide along with a simple example.

### Step-by-Step Guide

1. **Create a Context:**
   - Use `createContext` to create a context object.
   ```javascript
   import { createContext } from 'react';

   export const MyContext = createContext('default value');
   ```

2. **Provide a Context:**
   - Use the context provider to wrap your components that need access to the context.
   ```javascript
   function App() {
     return (
       <MyContext.Provider value={{ user: 'Aliyas' }}>
         <MyComponent />
       </MyContext.Provider>
     );
   }
   export default App;
   ```

3. **Consume a Context:**
   - Use `useContext` to consume the context within a component.
   ```javascript
   import React, { useContext } from 'react';
   import { MyContext } from '../App';

   const MyComponent = () => {
     const contextValue = useContext(MyContext);
     return (
       <div>
         Hello, {contextValue.user}!
       </div>
     );
   };
   export default MyComponent;
   ```

### Example with Notes

Here's the example you provided with explanations:

1. **Creating and Exporting Context:**
   - `createContext` creates a new context with a default value of `'aliyas'`.
   ```javascript
   import { createContext } from 'react';
   import './App.css';

   export const DAl = createContext('aliyas');
   ```

2. **Providing Context in App Component:**
   - The `DAl.Provider` is used to wrap the content inside the `App` component, providing the context value to its children. 
   - Note: The provider should be used with `.Provider` and should pass the `value` prop.
   ```javascript
   function App() {
     return (
       <>
         <DAl.Provider value={{ DAl: 'Aliyas' }}>
           <div className='flex justify-center'>
             Hello, {DAl}
           </div>
         </DAl.Provider>
       </>
     );
   }
   export default App;
   ```

3. **Consuming Context in a Component:**
   - `useContext(DAl)` is used to get the value provided by `DAl.Provider`.
   - The component displays the context value.
   ```javascript
   import React, { useContext } from 'react';
   import { DAl } from '../App';

   const Com = () => {
     const value = useContext(DAl);
     return (
       <div>
         Hello, {value.DAl}!
       </div>
     );
   };

   export default Com;
   ```

### Key Points:
- `createContext` is used to create a context.
- `useContext` is used to consume the context.
- The context provider (`<Context.Provider>`) wraps the components that need access to the context.
  
### Example With `Usestate`
`APP CONTENT`

   ```jsx
  import { createContext,useState } from 'react'
  import './App.css'
  import Com from './component/com'
  export const DAl = createContext(0)
  function App() {
    const [count, setcount] = useState(0)
    return (
      <>
      <DAl.Provider value={count}>
        <div className='flex justify-center'>
          <button onClick={()=>setcount(count+1)}>{count}</button>
          <Com/>
        </div>
        </DAl.Provider>
      </>
    )
  }
  export default App
  ```
Other content
  ```jsx
  import React, { useContext } from 'react'
  import { DAl } from '../App'
  const com = () => {
      const value = useContext(DAl)
      return (
          <div>
              {value}
          </div>
    )
  }
  
 export default com
  ```
### With all the buttons Working
App Content
   ```jsx
   import { createContext, useState } from 'react';
   import './App.css';
   import Com from './component/com';
   import LEX from './component/LEX';
   
   export const DAl = createContext();
   
   function App() {
     const [count, setcount] = useState(0);
   
     return (
       <>
         <DAl.Provider value={{ count, setcount }}>
           <div className='border border-black p-10'>
             <button onClick={() => setcount(count + 1)}>{count}</button>
             <LEX />
             <Com />
           </div>
         </DAl.Provider>
       </>
     );
   }
   
   export default App;
   ```
Other Content

   ```jsx
   import React, { useContext } from 'react';
   import { DAl } from '../App';
   
   const Com = () => {
     const { count, setcount } = useContext(DAl);
   
     return (
       <div className='border border-black p-10'>
         <button onClick={() => setcount(count + 1)}>Increment from Com</button>
         <p>Count: {count}</p>
       </div>
     );
   }
   
   export default Com;
   ```
Other content

   ```jsx
   import React, { useContext } from 'react';
   import { DAl } from '../App';
   
   const LEX = () => {
     const { count, setcount } = useContext(DAl);
   
     return (
       <div className='border border-black p-10'>
           <button onClick={()=>setcount(count+1)}>increase</button>
         <p>Count from LEX: {count}</p>
       </div>
     );
   }
   
   export default LEX;
   ```

This guide should help you quickly get started with the `useContext` hook in React.

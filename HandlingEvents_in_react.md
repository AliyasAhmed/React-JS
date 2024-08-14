## Handling Events in React Functional Components

### Definition
Handling events in React functional components involves defining a function and passing it as an event handler to an element.

### Example of Handling Events

1. **Basic Event Handling**

In a functional component, you can handle events like `onClick`, `onChange`, and others by defining a function and passing it as an event handler.

```jsx
import React from 'react';

function App() {
  // Define the event handler function
  const handleClick = () => {
    alert('Button clicked!');
  };

  return (
    <div>
      {/* Attach the event handler to the button */}
      <button onClick={handleClick}>Click Me</button>
    </div>
  );
}

export default App;
```

In this example, clicking the button will trigger the `handleClick` function, displaying an alert message.

2. **Event Handling with Parameters**

If you need to pass parameters to the event handler, you can use an arrow function.

```jsx
import React from 'react';

function App() {
  // Define the event handler function with parameters
  const handleClick = (message) => {
    alert(message);
  };

  return (
    <div>
      {/* Attach the event handler with parameters using an arrow function */}
      <button onClick={() => handleClick('Button clicked with parameter!')}>
        Click Me
      </button>
    </div>
  );
}

export default App;
```

In this example, clicking the button will trigger the `handleClick` function with the parameter `'Button clicked with parameter!'`.

### Summary
- **Event Naming**: React events are named using camelCase (e.g., `onClick` instead of `onclick`).
- **Event Handlers**: Pass a function as the event handler instead of a string.
- **Parameters**: Use arrow functions to pass parameters to event handlers.

These examples show how to handle events in React functional components in a simple and straightforward way.


# Handling Events and Forms in React

### Code Example

```jsx
import { useState } from 'react';
import reactLogo from './assets/react.svg';
import viteLogo from '/vite.svg';
import './App.css';

function App() {
  const [count, setCount] = useState(0);
  const [form, setForm] = useState({});

  const handleClick = () => {
    alert("Hey I am clicked");
  };

  const handleMouseOver = () => {
    alert("Hey I am a mouse over");
  };

  const handleChange = (e) => {
    setForm({ ...form, [e.target.name]: e.target.value });
    console.log(form);
  };

  return (
    <>
      <div className="button">
        <button onClick={handleClick}>Click me</button>
      </div>

      {/* <div className="red" onMouseOver={handleMouseOver}>
        I am a red div
      </div> */}

      <input type="text" name="email" value={form.email ? form.email : ""} onChange={handleChange} />
      <input type="text" name="phone" value={form.phone ? form.phone : ""} onChange={handleChange} /> 
    </>
  );
}

export default App;
```

### Notes

1. **Importing Required Modules**:
   ```javascript
   import { useState } from 'react';
   import reactLogo from './assets/react.svg';
   import viteLogo from '/vite.svg';
   import './App.css';
   ```
   - `useState` is a React hook for managing state.
   - Importing logos and CSS for styling.

2. **Setting Up State**:
   ```javascript
   const [count, setCount] = useState(0);
   const [form, setForm] = useState({});
   ```
   - `count` and `setCount` manage a simple counter (not used in this example).
   - `form` and `setForm` manage the state of form inputs.

3. **Event Handlers**:
   ```javascript
   const handleClick = () => {
     alert("Hey I am clicked");
   };

   const handleMouseOver = () => {
     alert("Hey I am a mouse over");
   };

   const handleChange = (e) => {
     setForm({ ...form, [e.target.name]: e.target.value });
     console.log(form);
   };
   ```
   - `handleClick`: Alerts when the button is clicked.
   - `handleMouseOver`: Alerts when the mouse is over the (commented-out) div.
   - `handleChange`: Updates the form state when the input value changes and logs the form state to the console.

4. **Rendering Elements**:
   ```javascript
   return (
     <>
       <div className="button">
         <button onClick={handleClick}>Click me</button>
       </div>

       {/* <div className="red" onMouseOver={handleMouseOver}>
         I am a red div
       </div> */}

       <input type="text" name="email" value={form.email || ""} onChange={handleChange} />
       <input type="text" name="phone" value={form.phone || ""} onChange={handleChange} /> 
     </>
   );
   ```
   - A button with an `onClick` event.
   - Two input fields for "email" and "phone" with `onChange` events.
   - A commented-out div for a `onMouseOver` event.

### Summary
- **State Management**: Use `useState` to manage component state.
- **Event Handling**: Define functions to handle events like click, mouse over, and input change.
- **Form Handling**: Use the `handleChange` function to update the form state dynamically based on input changes.

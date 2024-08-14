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

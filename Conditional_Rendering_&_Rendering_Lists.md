# Conditional Rendering

**Definition:** Conditional rendering in React means displaying different components or elements based on certain conditions, using JavaScript logic within JSX.

**1. Using Logical AND Operator (&&):**

The logical AND operator (`&&`) is used to render a component only if a condition is true. It's similar to an `if` statement but without an `else` case.

**Example:**

```jsx
import React, { useState } from 'react';

const App = () => {
  const [isActive, setIsActive] = useState(true);

  return (
    <div>
      <h1>Active User</h1>
      {isActive && <p>User is Active Now.....</p>}
    </div>
  );
}

export default App;
```

- If `isActive` is `true`, the message "User is Active Now....." is displayed.
- If `isActive` is `false`, nothing is displayed for that condition.

**2. Using Ternary Operator (?:):**

The ternary operator (`?:`) is used to render one component when a condition is true and another component when it's false. It's similar to an `if-else` statement.

**Example:**

```jsx
import React, { useState } from 'react';

const App = () => {
  const [isActive, setIsActive] = useState(true);

  return (
    <div>
      <h1>Active User</h1>
      {isActive ? <p>User is Active Now.....</p> : <p>User is Offline Now...</p>}
    </div>
  );
}

export default App;
```

- If `isActive` is `true`, the message "User is Active Now....." is displayed.
- If `isActive` is `false`, the message "User is Offline Now..." is displayed.

### Rendering Lists

**Definition:** Rendering lists in React involves looping through arrays or arrays of objects and displaying each item, usually with the `map` function.

**Example:**

```jsx
import React from 'react';

const App = () => {
  const todos = [
    { id: 0, title: "Go to Gym" },
    { id: 1, title: "Make Tea" },
  ];

  return (
    <ul>
      {todos.map((todo) => (
        <li key={todo.id}>{todo.title}</li>
      ))}
    </ul>
  );
}

export default App;
```

- The `todos` array contains objects with `id` and `title` properties.
- The `map` function loops through each `todo` and returns an `<li>` element.
- The `key` attribute is set to `todo.id` to uniquely identify each item.

**Why not use indexes as keys?**

Using indexes as keys is an anti-pattern because:

- When items are added or removed, indexes can change, causing unnecessary re-renders.
- Unique keys help React keep track of items more efficiently and avoid performance issues.

### Summary

- **Conditional Rendering**: Use the logical AND operator (`&&`) for simple conditions without an else case, and the ternary operator (`?:`) for conditions with both true and false cases.
- **Rendering Lists**: Use the `map` function to render lists dynamically, and always use unique keys (not indexes) to avoid unnecessary re-renders.

By understanding these concepts, you can create more dynamic and efficient React applications. If you have any more questions or need further examples, feel free to ask!

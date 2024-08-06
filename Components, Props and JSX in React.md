# Getting Started
## Overview
Vite (French word for "quick", pronounced /vit/, like "veet") is a build tool that aims to provide a faster and leaner development experience for modern web projects. It consists of two major parts:

A dev server that provides rich feature enhancements over native ES modules, for example extremely fast Hot Module Replacement (HMR).

A build command that bundles your code with Rollup, pre-configured to output highly optimized static assets for production.

Vite is opinionated and comes with sensible defaults out of the box. Read about what's possible in the Features Guide. Support for frameworks or integration with other tools is possible through Plugins. The Config Section explains how to adapt Vite to your project if needed.

```terminal
npm create vite@latest
```

Then install
```terminal
npm i
```

Then we would see npm node modules and then we have to run 
```
npm run dev
```
to start the server

Edit `src/App.jsx` and save to test HMR

# Basic app syntax

```jsx
function App() {
  const [count, setCount] = useState(0)

  return (
    <>
    whatever we write here will show on server
    </>
  )
}

export default App
```
### React Notes: Components, Props, and JSX

#### Components
- **Definition**: Reusable building blocks in a React app.
- **Example**: `Navbar`, `Card`, and `Footer` are components in your app.

#### Props
- **Definition**: Short for "properties," used to pass data to components.
- **Example**: In `Card`, `title` and `description` are props.

#### JSX (JavaScript XML)
- **Definition**: Syntax extension for JavaScript that looks like HTML.
- **Usage**: Used to define the UI structure in components.

### Example Code

**App Component**
```jsx
import Footer from './components/Footer';
import Navbar from './components/navbar';
import Card from './components/Card';

function App() {
  return (
    <>
      <Navbar />
      <Card title='card 1' description='card description' />
      <Footer />
    </>
  );
}

export default App;
```

**Card Component**
```jsx
import React from "react";
import './Card.css';

const Card = (props) => {
  return (
    <div className="Card">
      <h1>{props.title}</h1>
      <p style={{border:'2px solid black'}}>{props.description}</p>
    </div>
  );
}

export default Card;
```

**Footer Component**
```jsx
import React from 'react';
import './Footer.css';

const Footer = () => {
  return (
    <div className='footer'>
      copyright with Aliyas
    </div>
  );
}

export default Footer;
```

**Navbar Component**
```jsx
import React from 'react';
import './navbar.css';

const Navbar = () => {
  return (
    <div>
      <nav>
        <ul>
          <li>Home</li>
          <li>Projects</li>
          <li>About</li>
        </ul>
      </nav>
    </div>
  );
}

export default Navbar;
```

### CSS
- **Card**: 
  ```css
  .Card {
    border: 1px solid black;
    width: 20vw;
    margin: 34px;
    height: 40vh;
    display: flex;
    justify-content: center;
    align-items: center;
  }
  ```

- **Footer**:
  ```css
  .footer {
    background-color: rgb(56, 56, 56);
    text-align: center;
    position: fixed;
    bottom: 0;
    color: rgb(0, 0, 0);
    width: 100vw;
  }
  ```

- **Navbar**:
  ```css
  ul {
    display: flex;
    list-style: none;
    gap: 50px;
    color: rgb(235, 235, 235);
    background-color: rgb(53, 53, 53);
    margin: 10px;
    padding: 10px;
  }
  ```

Feel free to ask if you need more details!
                                    

# Rules to Follow
- We should use `classname=anything` not `class`

# Props Defining
```jsx
<Card title = 'card 1' description = 'card description'/>
```
Then we define Props `(properties)`

```jsx
const Card = (props) => {
```

### Whatever Changes we make in the main file would be applied everywhere.

# Inline Css in jsx
```jsx
style={{border:'2px solid black'}}
```
### Note That This is not Normal inline css we are defining a javascript in css so it is diffrent


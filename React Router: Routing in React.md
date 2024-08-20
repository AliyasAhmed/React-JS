### What is React Router?

React Router is a tool that helps you navigate between different pages in a React application without refreshing the entire page. Think of it as a way to show different content based on the URL, just like you would on a regular website.

### Components Explained

First, let's look at some simple React components:
First install React Router
   ```
   npm i react-router-dom
   ```
1. **Home Component**:
   ```jsx
   import React from 'react'

   const Home = () => {
     return (
       <div>
           <img src="https://images.pexels.com/photos/326055/pexels-photo-326055.jpeg?      
            auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1" alt="" />
         This is Home
       </div>
     )
   }
   


   export default Home
   ```

   - This component just displays "This is Home".

2. **About Component**:
   ```jsx
   import React from 'react'
   
   const About = () => {
     return (
       <div>
           <img src="https://images.pexels.com/photos/33045/lion-wild-africa-african.jpg? 
            auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1" alt="" />
         This is about
       </div>
     )
   }
   
   export default About
   ```

   - This component just displays "This is about".

3. **Login Component**:
   ```jsx
   import React from 'react'
   
   const Login = () => {
     return (
       <div>
           <img src="https://images.pexels.com/photos/1563355/pexels-photo-1563355.jpeg? 
            auto=compress&cs=tinysrgb&w=1260&h=750&dpr=1" alt="" />
         This is login
       </div>
     )
   }
   
   export default Login
   ```

   - This component just displays "This is login".

### Navbar Component

The Navbar helps users navigate between different pages:

```jsx
import React from 'react'
// import { Link } from 'react-router-dom' //in order to not get a refresh whenever we change the page we use link instead of <a></a> in React 
import { NavLink } from 'react-router-dom' // with navlink we can write functions in link
const Navbar = () => {
  return (
    <div className='flex list-none gap-10 p-7 content-center'>
      <nav className='flex gap-10'>
        <NavLink className={({ isActive }) => isActive ? "bg-slate-600 text-white p-5 rounded" : "text-White-800 p-5"} to='/Home'>Home</NavLink>
        <NavLink className={({ isActive }) => isActive ? "bg-slate-600 text-white p-5 rounded" : "text-White-800 p-5"} to='/About'>About</NavLink>
        <NavLink className={({ isActive }) => isActive ? "bg-slate-600 text-white p-5 rounded" : "text-White-800 p-5"} to='/Login'>Login</NavLink>
        
      </nav>
    </div>
  );
};

export default Navbar;

```

- **NavLink** is a special link that helps change the URL without refreshing the page.
- The `to` attribute defines the URL path.

### User Component with Dynamic URL

The User component shows different content based on the URL parameter:

```jsx
import React from 'react'
import { useParams } from 'react-router-dom'

const User = () => {
  const params = useParams()
  return (
    <div>
      I am user {params.username}
    </div>
  )
}

export default User
```

- **useParams**: This hook gets the parameters from the URL. If the URL is `/user/Alice`, `params.username` will be `Alice`.

### App Component - Setting Up Routes

The App component sets up the routes:

```jsx
import React from 'react'
import Navbar from './components/navbar'
import { createBrowserRouter, RouterProvider } from 'react-router-dom' // This is used to route between multiple pages withour refreshing
import Home from './components/home'
import Login from './components/login'
import About from './components/About'
import User from './components/User'

const App = () => {
  const router = createBrowserRouter([
    {
      path:'/Home', //This is how we make multiple paths
      element:<> <Navbar/> <Home/></>
    },
    {
      path:'/login',
      element:<> <Navbar/> <Login/></>
    },
    {
      path:'/about',
      element:<> <Navbar/> <About/></>

    },
    {
      path:'/user/:username',
      element:<> <Navbar/> <User/></>

    }
])
  return (
    <div>
      
      <RouterProvider router={router}/> 
    </div>
  )
}

export default App
```

- **createBrowserRouter**: This function defines different routes for your application.
  - `path`: The URL path (e.g., `/Home`).
  - `element`: The component(s) to show when the path matches.
- **RouterProvider**: This wraps the application and makes the routing work.

### Putting It All Together

1. When you navigate to `/Home`, the Home component will be displayed along with the Navbar.
2. When you navigate to `/About`, the About component will be displayed along with the Navbar.
3. When you navigate to `/Login`, the Login component will be displayed along with the Navbar.
4. When you navigate to `/user/John`, the User component will be displayed with "I am user John" along with the Navbar.

### Summary

- **React Router** helps navigate between different pages in your app without refreshing.
- **Components** are displayed based on the URL path.
- **NavLink** helps create navigation links.
- **useParams** gets URL parameters to display dynamic content.

This setup allows you to create a smooth, single-page application where the content changes without reloading the page, just like on a regular website.

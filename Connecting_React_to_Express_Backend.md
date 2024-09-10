# Connecting React to Express Backend

### 1. Install `cors` using `npm i cors` and `body-parser` using `npm i body-parser`

### 2. Write backend `Express Code` 

```jsx
import express from "express";
import cors from "cors";
import bodyParser from 'body-parser';

const app = express();
const port = 3000;

app.use(cors());
app.use(bodyParser.json());

app.get('/', (req, res) => {
    res.send('hello world');
});

app.post('/', (req, res) => {
    console.log(req.body);  
    //The line `console.log(req.body);` prints the data sent in the request body to the console. 
    //When a user submits a form on the frontend, this data (like username and password) is sent to the server. `req.body` holds this data, and `console.log(req.body);` lets you see it in the terminal to check if it was received correctly.
    res.send('Received data');
});

app.listen(port, () => {
    console.log(`Example app listening on port ${port}`);
});

```

`app.use(cors()):` Allows requests from other origins.
`app.use(bodyParser.json()):` Parses incoming JSON data into req.body.


### 3. run backend ` node .\backend\express.js` backend is folders name and express.js is js file

### 4. On Frontend side we already made the form then we connect with backend
```jsx
const submit = async (data) => {
  let r = await fetch("http://localhost:3000/", {method: "POST",  headers: {  // in submit part we will fetch the local host the is running on backend like this alsp the method will be post.
    let res = await r.text()
      "Content-Type": "application/json", 
    }, body: JSON.stringify(data)})
    let res = await r.text()
    console.log(data, res)// this will console the data we just fetched
```

### This code snippet is part of a `fetch` request that sends data from the frontend to the backend.


- **`headers`**: Tells the server that the data being sent is in **JSON** format.  
  `"Content-Type": "application/json"` makes it clear that we are sending JSON data.

- **`body`**: The actual data being sent to the server.  
  `JSON.stringify(data)` converts the `data` (like form inputs) into a JSON string format, which is needed for it to be sent properly.

In simple terms, this setup ensures that the server knows what type of data it is receiving and formats it correctly for transmission.


### Full Code
```jsx

import React from 'react'
import { useForm } from 'react-hook-form'

const App = () => {
  const { register, handleSubmit, watch, setError, formState: { errors, isSubmitting } } = useForm();
  const submit = async (data) => {
    // await delay(2)
    let r = await fetch("http://localhost:3000/", {method: "POST",  headers: {
      "Content-Type": "application/json", 
    }, body: JSON.stringify(data)})
    let res = await r.text()
    console.log(data, res)
  }
  const delay = (d) => {
    return new Promise((res, rej) => {
      setTimeout(() => {
        res()
      }, d * 1000);
    })
  }
  return (
    <>
      <div>
        <div className='flex justify-center items-center min-h-screen'>
          <form onSubmit={handleSubmit(submit)} className='flex flex-col items-center border border-gray-700 p-[5rem] rounded-lg shadow'>
            <p>username</p>
            <input type="text" {...register('username', {required:{value:true, message:'this field is required' },minLength:{value:3, message:'atleast Three characters required'}, maxLength:{value:10, message:'only 10 characters are allowerd'}})} placeholder='username' className='bg-[#4949496b] p-2 w-[15rem] rounded-r-sm my-10' />
            {errors.username && <div className='text-red-700'>{errors.username.message}</div>}
            <p>password</p>
            <input type="text" {...register('password')} placeholder='password' className='bg-[#4949496b] p-2 w-[15rem] rounded-r-sm' />
            <input disabled={isSubmitting} className='bg-slate-700 p-2 mt-6 rounded-lg hover:bg-slate-600 transition-all cursor-pointer' type="submit" value="submit" />
          </form>
        </div>
      </div>
    </>
  )
}

export default App
```

### Backend
```jsx
import express from "express";
import cors from "cors";
import bodyParser from 'body-parser';

const app = express();
const port = 3000;

app.use(cors());
app.use(bodyParser.json());

app.get('/', (req, res) => {
    res.send('hello world');
});

app.post('/', (req, res) => {
    console.log(req.body);  // Correctly logs form data
    res.send('Received data');
});

app.listen(port, () => {
    console.log(`Example app listening on port ${port}`);
});
```

In the line `console.log(data, res)`, `res` refers to the response object received from the server after making a request.

Here's a breakdown:

1. **`data`**: This is the data you sent from your React app, which is logged to show what was sent.

2. **`res`**: This is the response you receive from the server after sending the request. It represents the server's reply.

### What `res` Contains

- **`res.text()`**: If you use `res.text()`, it converts the server's response to a plain text string.
- **`res.json()`**: If the server responds with JSON, you can use `res.json()` to parse it.

### Example Usage

In your `submit` function:

```javascript
const submit = async (data) => {
  let response = await fetch("http://localhost:3000/", {
    method: "POST",
    headers: { "Content-Type": "application/json" },
    body: JSON.stringify(data)
  });
  let result = await response.text();  // Converts response to text
  console.log(data, result);  // Logs both the sent data and the server's response
};
```

- **`data`**: Shows the form data sent to the server.
- **`result`**: Shows what the server sent back in response (converted to text).

So, `console.log(data, res)` will output both the data sent to the server and the server's reply.

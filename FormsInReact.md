# React Forms
#### why do we use react form, it makes it easier to make forms and we dont have to write multiple line of code to make it.

### Step by Step Guide

1. we import this
    ```jsx
    import { set, useForm } from "react-hook-form"
    ```
2. we make a hook of `useform()`
    ```jsx
    const { register, handleSubmit, watch, setError, formState: { errors, isSubmitting } } = useForm();
    // register, handleSubmit, watch, setError, formState: { errors, isSubmitting} these are the things we would
    // would use to make a basic form 
    ```
3. when we do this `{...register("username")}` then we dont require this anymore  `name='username' id=''` 
    ```jsx
    input placeholder='username' {...register("username")
    ```
### 4. `onSubmit` Function Definition

```javascript
const onSubmit = async (data) => { ... };
```

- **`onSubmit` function**: This function is called when the form is submitted. It takes `data` as an argument, which contains all the form input values.

- **`await delay(2)`**: This line simulates a network delay of 2 seconds using the `delay` function.

- **`console.log(data)`**: This line logs the form data to the console for debugging purposes.

- **`setError` calls**: These lines set custom error messages based on the submitted username:
  - If the username is not `'aliyas'`, it sets an error for `'myform'`.
  - If the username is `'ahmed'`, it sets an error indicating the user is blocked.


5. if we use `{required : true }` it means this filed is required and you cant submit without filling it up. As well            as for the `minlength` and `max length` we can do same thing `{required : true, minlength: 3, maxlength: 8}`       
   remember this is an `object` that the reasone we are using it like this `{argument:value}`.
     
    ```jsx
    <input placeholder='username' {...register("username", { required: { value: true, message: 'this field is required' },
  
    minLength: { value: 3, message: 'min length is 3' }, maxLength: { value: 8, message: 'max value should be more than 8' } })}   type="text" />
    ```
6. As we used the the `require`, `max` and `min` field we have catch the `errors` if the requirement is not filled, for that we will use `errors` that we already imported.
   
    ```jsx
    formState: { errors, isSubmitting } } = useForm();
    ```
7. We can use errors like this `{errors.username && <div>There is some error in username </div> }` bellow the filed 
   that contains requirement and other stuff and we use div to implement out message

    ```jsx
    <input placeholder='username' {...register("username", { required: { value: true, message: 'this field is required' },
    minLength: { value: 3, message: 'min length is 3' }, maxLength: { value: 8, message: 'max value should be more than 8'}
    })} type="text" className="mb-4 bg-[#5050504f] text-white p-2 mx-4 rounded-lg" />
    {errors.username && <div className='text-red-500'>{errors.username.message}</div>}
    // every input will contains its own errors object like this so it show errors for each input seperately
    ```
8. Also instead of this `{minLength : 3, maxLength : 8}` we can show the message for indidual objeccts like this
   
   ```jsx
   minLength: { value: 3, message: 'min length is 3' }, maxLength: { value: 8, message: 'max value should be more than 8' }
   ```
      `{minLength : 3, maxLength : 8}` => `{minLength : {value:3, message:'min length is 3'}`, `maxLength : {value : 8, message: 'max value should be more than 3'}`, 
      like this we make object of object and display messages but now we have to show the message we have to change previous div from `<div>There is some error in username </div> }` to `<div>{errors.username}<div/>` so it would show all the error messages

9. same thing can be done with require object which contains true => {required : true} instead we can do this so the message of error would show up. `{required : {value:true, message: 'this field is required'}`.
   
    ```jsx
    {required : {value:true, message: 'this field is required'}
    ```
10. We can also add a delay to submit so people wont be able to click multiple time when submitting a form
    
      ```jsx
        const delay = (d) => {
          return new Promise((resolve, reject) => {
            setTimeout(() => {
              resolve()
            }, d * 1000); // d * 1000 because if we only use 1000 it would stuck of 1 sec and we would be able to change it.
          })
        }
      ```
11. Next we can do is disable the submit button so we would be able to click it only once at a time.
we have to make a function for that in `submit button`, but we have to make it in `formstate` because its not a `function` its a `value` , `formState: { errors, isSubmitting }` like this so in our input we will use `disabled = {isSubmitting}`.
    
      ```jsx
      <input disabled={isSubmitting} type="submit" value="submit"/>
      ```
      
12. `{isSubmitting && <div>Loading...</div>}` so basically we said if isSubmitting is true show Loading.. so when the isSubmitting value is true the button will be disabled and loading will show up
    
      ```jsx
      {isSubmitting && <div>Loading...</div>} //so basically we said if isSubmitting is true show Loading.. 
      ```
      
13. now in password we would do same as we did in username to show errors .
    
    ```jsx
    {...register("password", {required: {value:true, message: 'This field is required'}, minLength: {value:3, message:"atleast 
    three characters "}
    ```

14. In Order to get custome errors we have added new line of code `{errors.myfrom && <div className='text-red-500'>{errors.myfrom.message}</div> }` right below the input submit we have to make a function if setError in the useFrom hook.
    
    ```jsx
    <input disabled={isSubmitting} type="submit" value="submit" />
    {errors.myform && <div className='text-red-500'>{errors.myform.message}</div>}
    ```

15. first we make setError in the hook to get custome errors then we write this in the onSubmit button
    
    ```jsx
    const onSubmit = async (data) => {
      await delay(2) // for network delay 
      console.log(data)
      if (data.username !== 'aliyas') {
        setError('myform', { message: 'username is invalid' }) // myform is custom name here for the error we can set anything and message should be object.
      }
    };
    ```
16. Then `{errors.myform && <div className='text-red-500'>{errors.myform.message}</div> }` below the input submit also we canwrite anything instead of my form but the message should be in object.


17. we made another custome error by the name of ahmed which is a blocked user so we would follow same process. In Total It looks like this

    ```jsx
        const onSubmit = async (data) => {
        await delay(2) // for network delay 
        console.log(data)
        if (data.username !== 'aliyas') {
          setError('myform', { message: 'username is invalid' }) // tHis is for the username validation
        }
        if (data.username === 'ahmed') {
          setError('ahmed', { message: 'sorry this user is blocked' }) // this is also for usernmae validation
        }
      };
    ```


# **Full Code**


```jsx
    import React from 'react'
    import { set, useForm } from "react-hook-form"
    
    const App = () => {
      const { register, handleSubmit, watch, setError, formState: { errors, isSubmitting } } = useForm();
    
      const delay = (d) => {
        return new Promise((resolve, reject) => {
          setTimeout(() => {
            resolve()
          }, d * 1000);
        })
      }
      const onSubmit = async (data) => {
        await delay(2) // for network delay 
        console.log(data)
        if (data.username !== 'aliyas') {
          setError('myform', { message: 'username is invalid' })
        }
        if (data.username === 'ahmed') {
          setError('ahmed', { message: 'sorry this user is blocked' })
        }
      };
      return (
        <>
    
          <div className="min-h-screen flex items-center justify-center">
            <div className=" border border-gray-800 p-9 rounded-lg shadow-xl shadow-slate-700 ">
              {isSubmitting && <div>Loading...</div>}
              <form onSubmit={handleSubmit(onSubmit)} className='container flex flex-col items-center'>
                <p className='pb-5'>Username</p>
                <input placeholder='username' {...register("username", { required: { value: true, message: 'this field is required' }, minLength: { value: 3, message: 'min length is 3' }, maxLength: { value: 8, message: 'max value should be more than 8' } })} type="text" className="mb-4 bg-[#5050504f] text-white p-2 mx-4 rounded-lg" />
                {errors.username && <div className='text-red-500'>{errors.username.message}</div>}
                <br />
                <p className='pb-5'>Password</p>
                <input placeholder='password' {...register("password", { required: { value: true, message: 'This field is required' }, minLength: { value: 3, message: "atleast three characters " } })} type="password" className="mb-4 bg-[#5050504f] text-white p-2 mx-4 rounded-lg" />
                {errors.password && <div className='text-red-500'>{errors.password.message}</div>}
                <br />
                <input disabled={isSubmitting} type="submit" value="submit" className="mb-4 bg-slate-900 rounded-lg cursor-pointer p-3 hover:bg-slate-800" />
                {errors.myform && <div className='text-red-500'>{errors.myform.message}</div>}
                {errors.ahmed && <div className='text-red-500'>{errors.ahmed.message}</div>}
              </form>
            </div>
          </div>
        </>
      )
    }
    
    export default App
```
### Questions

The key reason we don't use `onSubmit` on the `<input type="submit" />` element is because of how HTML forms and React work together. Let's break it down.

### Why Not Use `onSubmit` on `<input type="submit" />`?

1. **HTML Form Behavior**: In HTML, the `<form>` element is what handles form submissions, not the `<input type="submit" />`. When you click the submit button, the form itself triggers the `submit` event, not the button.

2. **`onSubmit` Event**: The `onSubmit` event must be placed on the `<form>` tag. This is because when you submit a form (either by clicking a submit button or pressing the Enter key), the browser looks for an `onSubmit` event handler on the form element. If it's placed on the button, it won't be triggered as you might expect.

3. **React `handleSubmit` Function**: The `handleSubmit` function provided by `react-hook-form` is specifically designed to be used with the form's `onSubmit` event. It wraps around your custom `submit` function to handle validation and prevent the default browser behavior (like refreshing the page).

### Why Do We Use `handleSubmit` on the `<form>` Tag?

- **Validation**: The `handleSubmit` function ensures that all validations you've set up using `register` are checked before calling your custom submit function (`onSubmit` in this case). If you put `onSubmit` on the `<input type="submit" />`, the validations won't be processed correctly.

- **Prevent Default Form Submission Behavior**: In a standard HTML form, when the form is submitted, the browser reloads the page by default. `handleSubmit` prevents this default behavior, allowing React to handle everything smoothly.

- **Handling Enter Key Presses**: When the user presses Enter in an input field, the form is submitted automatically. If `handleSubmit` is on the form, it will handle this correctly. If you put it on the submit button, pressing Enter won't trigger the form submission properly.

### Correct Approach

Here's why we correctly place `handleSubmit` on the `<form>`:

```jsx
<form onSubmit={handleSubmit(onSubmit)} className='container flex flex-col items-center'>
  {/* Form elements like input fields go here */}
  <input type="submit" value="submit" className='text-white bg-slate-700' />
</form>
```

- **`onSubmit={handleSubmit(onSubmit)}`**: This line on the `<form>` ensures that when the form is submitted (either by clicking the submit button or pressing Enter), it first checks for validation and then calls the `onSubmit` function.

### Summary

- **HTML Form Behavior**: Form submission is managed by the `<form>` element, not the `<input>` button.
- **`handleSubmit` on `<form>`**: This is required to perform validation, prevent default browser behavior, and handle all submission scenarios properly.
- **Incorrect Behavior on Button**: Placing `onSubmit` on the button won't trigger correctly when pressing Enter or handle form-level validation as needed.

By using `handleSubmit` on the form, you ensure everything works as expected in a React environment with `react-hook-form`.

# **What If We Don't Use React Form**

Certainly! The `...register` syntax in your code is used to spread the properties and methods returned by the `register` function from the [`react-hook-form`](https://react-hook-form.com/) library into the `input` element. This effectively "registers" the input field with the `react-hook-form` system, enabling form state management and validation.

Here's the relevant part of your code for reference:

```javascript
const { register, handleSubmit, watch, formState: { errors } } = useForm();

<form onSubmit={handleSubmit(onSubmit)} className='container flex flex-col items-center'>
  <input name="username" {...register("username")} className="mb-4 bg-gray-400 text-black" />
  <input name="password" {...register("password")} type="password" className="mb-4 bg-gray-400 text-black" />
  <input type="submit" value="submit" className="mb-4 bg-gray-400 cursor-pointer p-3" />
</form>
```

If you were not using `react-hook-form` and the `register` function, you would need to manually handle the state and validation for each input field. This would involve writing more code to manage the state, handle changes, and validate the inputs.

For example, without `react-hook-form`, you might have to do something like this:

```javascript
import React, { useState } from 'react';

const App = () => {
  const [formData, setFormData] = useState({ username: '', password: '' });
  const [errors, setErrors] = useState({});

  const handleChange = (e) => {
    setFormData({ ...formData, [e.target.name]: e.target.value });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    // Perform validation and submit the form
    if (formData.username === '') {
      setErrors({ ...errors, username: 'Username is required' });
    } else {
      console.log(formData);
    }
  };

  return (
    <form onSubmit={handleSubmit} className='container flex flex-col items-center'>
      <input
        name="username"
        value={formData.username}
        onChange={handleChange}
        className="mb-4 bg-gray-400 text-black"
      />
      {errors.username && <span>{errors.username}</span>}
      <input
        name="password"
        type="password"
        value={formData.password}
        onChange={handleChange}
        className="mb-4 bg-gray-400 text-black"
      />
      <input type="submit" value="submit" className="mb-4 bg-gray-400 cursor-pointer p-3" />
    </form>
  );
};

export default App;
```

As you can see, without `react-hook-form`, you need to manually handle the state and validation, which can be cumbersome and error-prone. The `register` function simplifies this process by automatically managing the state and validation for you.
        
        
        
Yes, you are correct. The `register` function from the `[react-hook-form](https://react-hook-form.com/)` library is an alternative to manually handling the `onChange` event and `e.target.value` for each input field.

When you use `register`, it automatically handles the state and validation for the input fields, which simplifies the code and reduces the amount of boilerplate you need to write.

Here's a comparison for clarity:

### Using `react-hook-form` with `register`:
```javascript
import React from 'react';
import { useForm } from 'react-hook-form';

const App = () => {
  const { register, handleSubmit, watch, formState: { errors } } = useForm();
  const onSubmit = data => console.log(data);

  return (
    <form onSubmit={handleSubmit(onSubmit)} className='container flex flex-col items-center'>
      <input name="username" {...register("username")} className="mb-4 bg-gray-400 text-black" />
      <input name="password" {...register("password")} type="password" className="mb-4 bg-gray-400 text-black" />
      <input type="submit" value="submit" className="mb-4 bg-gray-400 cursor-pointer p-3" />
    </form>
  );
};

export default App;
```

### Manually handling state and `onChange`:
```javascript
import React, { useState } from 'react';

const App = () => {
  const [formData, setFormData] = useState({ username: '', password: '' });

  const handleChange = (e) => {
    setFormData({
      ...formData,
      [e.target.name]: e.target.value
    });
  };

  const handleSubmit = (e) => {
    e.preventDefault();
    console.log(formData);
  };

  return (
    <form onSubmit={handleSubmit} className='container flex flex-col items-center'>
      <input name="username" value={formData.username} onChange={handleChange} className="mb-4 bg-gray-400 text-black" />
      <input name="password" value={formData.password} onChange={handleChange} type="password" className="mb-4 bg-gray-400 text-black" />
      <input type="submit" value="submit" className="mb-4 bg-gray-400 cursor-pointer p-3" />
    </form>
  );
};

export default App;
```

In the first example, `react-hook-form`'s `register` function takes care of the state and validation, making the code cleaner and more concise. In the second example, you have to manually handle the state and `onChange` events for each input field.
        


# React Forms
### why do we use react form, it makes it easier to make forms and we dont have to write multiple line of code to make it.

### Step by Step Guide

1. we import this
  ```jsx
  import { set, useForm } from "react-hook-form"
  ```
2. we make a hook of `useform()`
   ```jsx
   const { register, handleSubmit, watch, setError, formState: { errors, isSubmitting } } = useForm();
   // register, handleSubmit, watch, setError, formState: { errors, isSubmitting} these are the things we would
    would use to make a basic form 
   ```
#### ** when we do this `{...register("username")}` then we dont require this anymore  `name='username' id=''` **
  ```jsx
     input placeholder='username' {...register("username")
  ```
####  if we use `{required : true }` it means this filed is required and you cant submit without filling it up. As well as for the minlength and max length we can do same thing {required : true, minlength: 3, maxlength: 8} remember this is an object that the reasone we are using it like this {argument:value}

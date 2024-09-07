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
  would use to make a basic form 
  ```
3. ####  when we do this `{...register("username")}` then we dont require this anymore  `name='username' id=''` 
  ```jsx
  input placeholder='username' {...register("username")
  ```
4. ####  if we use `{required : true }` it means this filed is required and you cant submit without filling it up. As well            as for the `minlength` and `max length` we can do same thing `{required : true, minlength: 3, maxlength: 8}`       
   remember this is an `object` that the reasone we are using it like this `{argument:value}`.
  ```jsx
  <input placeholder='username' {...register("username", { required: { value: true, message: 'this field is required' },

  minLength: { value: 3, message: 'min length is 3' }, maxLength: { value: 8, message: 'max value should be more than 8' } })}   type="text" />
  ```
#### As we used the the `require`, `max` and `min` field we have catch the `errors` if the requirement is not filled, for that we will use `errors` that we already imported.
  ```jsx
  formState: { errors, isSubmitting } } = useForm();
  ```
#### We can use errors like this `{errors.username && <div>There is some error in username </div> }` bellow the filed that contains requirement and other stuff and we use div to implement out message
  ```jsx
  <input placeholder='username' {...register("username", { required: { value: true, message: 'this field is required' },
  minLength: { value: 3, message: 'min length is 3' }, maxLength: { value: 8, message: 'max value should be more than 8'}
  })} type="text" className="mb-4 bg-[#5050504f] text-white p-2 mx-4 rounded-lg" />
  {errors.username && <div className='text-red-500'>{errors.username.message}</div>}
  // every input will contains its own errors object like this so it show errors for each input seperately
  ```

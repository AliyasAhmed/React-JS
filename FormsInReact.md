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
4. if we use `{required : true }` it means this filed is required and you cant submit without filling it up. As well            as for the `minlength` and `max length` we can do same thing `{required : true, minlength: 3, maxlength: 8}`       
   remember this is an `object` that the reasone we are using it like this `{argument:value}`.
     
    ```jsx
    <input placeholder='username' {...register("username", { required: { value: true, message: 'this field is required' },
  
    minLength: { value: 3, message: 'min length is 3' }, maxLength: { value: 8, message: 'max value should be more than 8' } })}   type="text" />
    ```
5. As we used the the `require`, `max` and `min` field we have catch the `errors` if the requirement is not filled, for that we will use `errors` that we already imported.
   
    ```jsx
    formState: { errors, isSubmitting } } = useForm();
    ```
6. We can use errors like this `{errors.username && <div>There is some error in username </div> }` bellow the filed 
   that contains requirement and other stuff and we use div to implement out message

    ```jsx
    <input placeholder='username' {...register("username", { required: { value: true, message: 'this field is required' },
    minLength: { value: 3, message: 'min length is 3' }, maxLength: { value: 8, message: 'max value should be more than 8'}
    })} type="text" className="mb-4 bg-[#5050504f] text-white p-2 mx-4 rounded-lg" />
    {errors.username && <div className='text-red-500'>{errors.username.message}</div>}
    // every input will contains its own errors object like this so it show errors for each input seperately
    ```
7. Also instead of this `{minLength : 3, maxLength : 8}` we can show the message for indidual objeccts like this
   
   ```jsx
   minLength: { value: 3, message: 'min length is 3' }, maxLength: { value: 8, message: 'max value should be more than 8' }
   ```
      `{minLength : 3, maxLength : 8}` => `{minLength : {value:3, message:'min length is 3'}`, `maxLength : {value : 8, message: 'max value should be more than 3'}`, 
      like this we make object of object and display messages but now we have to show the message we have to change previous div from `<div>There is some error in username </div> }` to `<div>{errors.username}<div/>` so it would show all the error messages

8. same thing can be done with require object which contains true => {required : true} instead we can do this so the message of error would show up. `{required : {value:true, message: 'this field is required'}`.
   
    ```jsx
    {required : {value:true, message: 'this field is required'}
    ```
9. We can also add a delay to submit so people wont be able to click multiple time when submitting a form
    
      ```jsx
        const delay = (d) => {
          return new Promise((resolve, reject) => {
            setTimeout(() => {
              resolve()
            }, d * 1000); // d * 1000 because if we only use 1000 it would stuck of 1 sec and we would be able to change it.
          })
        }
      ```
10. Next we can do is disable the submit button so we would be able to click it only once at a time.
we have to make a function for that in `submit button`, but we have to make it in `formstate` because its not a `function` its a `value` , `formState: { errors, isSubmitting }` like this so in our input we will use `disabled = {isSubmitting}`.
    
      ```jsx
      <input disabled={isSubmitting} type="submit" value="submit"/>
      ```
      
11. `{isSubmitting && <div>Loading...</div>}` so basically we said if isSubmitting is true show Loading.. so when the isSubmitting value is true the button will be disabled and loading will show up
    
      ```jsx
      {isSubmitting && <div>Loading...</div>} //so basically we said if isSubmitting is true show Loading.. 
      ```
      
12. now in password we would do same as we did in username to show errors .
    
    ```jsx
    {...register("password", {required: {value:true, message: 'This field is required'}, minLength: {value:3, message:"atleast 
    three characters "}
    ```

13. In Order to get custome errors we have added new line of code `{errors.myfrom && <div className='text-red-500'>{errors.myfrom.message}</div> }` right below the input submit we have to make a function if setError in the useFrom hook.
    
    ```jsx
    <input disabled={isSubmitting} type="submit" value="submit" />
    {errors.myform && <div className='text-red-500'>{errors.myform.message}</div>}
    ```

14. first we make setError in the hook to get custome errors then we write this in the onSubmit button
    
    ```jsx
    const onSubmit = async (data) => {
      await delay(2) // for network delay 
      console.log(data)
      if (data.username !== 'aliyas') {
        setError('myform', { message: 'username is invalid' }) // myform is custom name here for the error we can set anything and message should be object.
      }
    };
    ```
15. Then `{errors.myform && <div className='text-red-500'>{errors.myform.message}</div> }` below the input submit also we canwrite anything instead of my form but the message should be in object.


16. we made another custome error by the name of ahmed which is a blocked user so we would follow same process. In Total It looks like this

    ```jsx
        const onSubmit = async (data) => {
        await delay(2) // for network delay 
        console.log(data)
        if (data.username !== 'aliyas') {
          setError('myform', { message: 'username is invalid' }) // tHis is for the username validation
        }
        if (data.username === 'ahmed') {
          setError('ahmed', { message: 'sorry this user is blocked' }) this is also for usernmae validation
        }
      };
    ```

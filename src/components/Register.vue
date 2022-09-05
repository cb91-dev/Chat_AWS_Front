<template>
  <!--
    This example requires updating your template:

    ```
    <html class="h-full bg-gray-50">
    <body class="h-full">
    ```
  -->
  <div class="min-h-full flex items-center justify-center py-12 px-4 sm:px-6 lg:px-8">
    <div class="max-w-md w-full space-y-8">
       <div>
        <h1 class="text-green-500 text-5xl font text-center">Chat!</h1>
        <h2 class=" mt-6 text-center text-1xl  text-gray-400 py-4">Create your new account</h2>
      </div>
      <form class="mt-8 space-y-6" action="#" method="POST">
        <input type="hidden" name="remember" value="true" />
        <div class="rounded-md shadow-sm -space-y-px">
             <div>
            <label for="user_name" class="sr-only">User name</label>
            <input v-model="user_name" id="user_name" name="user_name" type="text" required="" class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-t-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm" placeholder="User name" />
          </div>
          <div>
            <label for="email-address" class="sr-only">Email address</label>
            <input v-model="new_email" id="new_email" name="email" type="email" autocomplete="email" required="" class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900  focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm" placeholder="Email address" />
          </div>
          <div>
            <label for="password" class="sr-only">Password</label>
            <input v-model="new_password" id="new_password" name="new_password" type="password" autocomplete="current-password" required="" class="appearance-none rounded-none relative block w-full px-3 py-2 border border-gray-300 placeholder-gray-500 text-gray-900 rounded-b-md focus:outline-none focus:ring-indigo-500 focus:border-indigo-500 focus:z-10 sm:text-sm" placeholder="Password" />
          </div>
        </div>

        <div class="py-4">

        </div>
         <p v-if="error" class="text-center text-red-400 text-sm">{{error.value}}</p>

        <div>
          <button @click.prevent="checkPasswordEmail" type="submit" class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-green-500 hover:bg-green-400 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
            <span class="absolute left-0 inset-y-0 flex items-center pl-3">
              <UserAddIcon class="h-5 w-5 text-white" aria-hidden="true" />
            </span>
            Register
          </button>
          <div class="py-2"></div>
               <button @click.prevent="backtologin" class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-blue-500 hover:bg-blue-700 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
            <span class="absolute left-0 inset-y-0 flex items-center pl-3">
              <ArrowLeftIcon class="h-5 w-5 text-white" aria-hidden="true" />
            </span>
            Back to login
          </button>
        </div>
      </form>
    </div>
  </div>
</template>



<script setup>
import { ArrowLeftIcon, UserAddIcon } from '@heroicons/vue/solid'

import { ref,reactive } from 'vue';


// used to switch form or relay response from regsiter function
const emit = defineEmits(['form_switch','response'])

const backtologin = () => {
    emit('form_switch','')
}
const user_name = ref("")
const new_email = ref("")
const new_password = ref("")
const error = reactive({})


// check pass/email strength 
const checkPasswordEmail = () => {
  //  checking value of user pword
  const regex_test = /^(?=.*\d)(?=.*[a-z])(?=.*[A-Z])(?=.*[a-zA-Z]).{8,}$/.test(new_password.value)
  //  checking value of user email
  const reg_email = /[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*@(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?/.test(new_email.value)
  if (regex_test == true && reg_email == true){
    // Passed reg user check !! 
    Regsiter()
  }
  else{
    error.value = "A vaild email and a password with at least eight characters with one number,one special character"  
  }
}


// Register function
const Regsiter = () => {
    const url = "http://127.0.0.1:8000/register";
    const options = {
    method: "POST",
    headers: {
        Accept: "application/json",
        "Content-Type": "application/json;charset=UTF-8",
    },
  body: JSON.stringify({
    user_name: user_name.value, 
    email: new_email.value,
    password: new_password.value,
  }),
};
fetch(url, options)
  .then((response) => response.json())
  .then((data) => {
      console.log(data.headers)
    if(data.status_code == 201){
      localStorage.setItem("JWT", data.headers);
      emit('response',true)
      return
    }
    if(data.status_code == 404){
      // not a register user
      error.value = data.detail
      return 
    }
     if(data.status_code == 422){
      // trying to catch werid error
      error.value = 'somthing has gone wrong'
      return 
    }
      if(data.detail){
      //catch not input from user error
      error.value = data.detail[0].msg
      return 
    }
    
  })
  .catch((error) => { console.error('Error:', error)
  });
}
</script>
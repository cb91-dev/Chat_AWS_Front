<template>

<div class="h-screen">
  <div class="flex justify-between h-10 p-2 border-b-2">
   <ArrowLeftIcon v-if="addChat.load" @click="ToggleAddChat" class="text-blue-500 self-center h-8"/>
  <!-- ADD Chat -->
    <UserCircleIcon v-else @click="ToggleAddChat" class="text-blue-500 self-center h-8"/>
    <div class="text-green-500 text-3xl font self-center">Chat!</div>
    <!-- LOG OUT -->
    <div @click="Logout" class="font text-red-500">log out
    </div>
  </div>
  <div>
    <UserProfile v-if="addChat.load"/>
    <Profiles v-else :users='users'/>
  </div>
</div>

</template>


<script setup>
import Profiles from './Profiles.vue'
import UserProfile from './UserProfile.vue'

import { ArrowLeftIcon, UserCircleIcon } from '@heroicons/vue/solid'
import { reactive } from 'vue';

//  Modal for adding new chat 
const ToggleAddChat = () => {
  addChat.load = !addChat.load
}

const addChat = reactive({
   load: false,
})


const emit = defineEmits(['controller'])


const Logout = () => {
        emit("controller" ,'logout')
        localStorage.clear()
        localStorage.removeItem("JWT")
}

const users = [
  {
  "user_name": "August King",
  "email": "rita61@swaniawski.info",
  "online": true,
  "last_msg": "Asperiores ut totam ab dolore velit maxime."
  },
   {
  "user_name": "Billy the Kid",
  "email": "billthekid@mil.com",
  "online": false,
  "last_msg": "Ea corporis sint reiciendis omnis quos doloremque hic. Tempore ea quidem odit."
  },
   {
  "user_name": "The Other Guy",
  "email": "tog@mail.com",
  "online": true,
  "last_msg": "Et at omnis mollitia possimus quis molestias incidunt."
  },
]


  
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Kanit&display=swap');

.font{
   font-family: 'Kanit', sans-serif;
}
</style>
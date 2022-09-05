<template>
<div class="">
        <div class="px-4">
        <form class="flex flex-col py-3">
            <label class="text-center" for="cars">Start a new Chat!</label>
            <div class="py-2"></div>
            <select id="cars" name="carlist" class="text-center rounded">
                <option value="volvo">Volvo</option>
                <option value="volvo">Volvo</option>
                <option value="volvo">Volvo</option>
            </select>
            <div class="py-2"></div>
              <button  type="submit" class="group relative w-full flex justify-center py-2 px-4 border border-transparent text-sm font-medium rounded-md text-white bg-blue-500 hover:bg-blue-400 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-indigo-500">
            <span class="absolute left-0 inset-y-0 flex items-center pl-3">
            </span>
            Start Chat
          </button>
        </form>    
        </div>
    </div>
    <div class="border-solid border-t-2 py-3 text-center">Current Chats</div>
<div  v-for="x in props.users" class=" py-1 px-2 border-b-2">
  <div key="x.user_name" class="shadow rounded ">
    <div @click='selectChat(x.user_name)' class="px-4 py-5 sm:p-6">
      <div >
        <div class="flex justify-between">
            <h3 class="text-lg leading-6 font-medium text-gray-900">{{x.user_name}}</h3>
            <div :class="[x.online ? 'text-xs inline-flex items-center px-1 py-1 border border-transparent shadow-sm rounded-md text-white bg-green-500 focus:ring-offset-2':'text-xs inline-flex items-center px-1 py-1 border border-transparent shadow-sm rounded-md text-white bg-indigo-700']">{{ x.online ? "Online" : "Offline" }}</div>
         </div>
          <div class="mt-2 max-w-xl text-sm text-gray-500">
            <p class="'text-xs">{{x.last_msg}}</p>
          </div>
      </div>
    </div>
  </div>
  </div>
  <div class="bg-slate-500/20 rounded p-1 absolute bottom-0 top-0 left-0 right-0"  v-if='chat.load'>
  <ChatBox class="absolute bottom-0  rounded top-1 left-5 right-5" @closeChat="controller" :chatUser="chatUser"/>
  </div>
    <div v-else>

    </div>
</template>



<script setup>
import ChatBox from './ChatBox.vue';
import { reactive } from 'vue';


const emit = defineEmits(['closeChat'])

const props = defineProps(['users'])


const chat = reactive({
   load: false,
})
const chatUser = reactive({
    user_name: 'load',
}) 

// Switch between chats 
const controller = (event) => {
    if (event == 'close'){
        chat.load = !chat.load
    }else {
    chat.load = chat.load
    }
}

// this will be a api call to fetch messages

const selectChat = (x) => {
    chatUser.user_name = x
    chat.load = true
 }


</script>


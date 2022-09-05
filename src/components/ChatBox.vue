<template>
    <div class="bg-white">
        <div>
        </div>
        <div class="rounded-t grid  grid-cols-3 gap-4 border-b-2 z-30">
            <div class="user-header text-green-500 self-center col-start-2 text-center">{{props.chatUser.user_name}}</div>
            <div class="flex justify-end">
            <XIcon @click.prevent="closeChat" class="col-end-4 text-red-600 h-8"/>
            </div>  
        </div>
        <!-- Messsages -->
        <div class="h-5/6 overflow-y-scroll bg-slate-50">
       <Messages class="overflow-hidden" v-for="{ user_name, msg, online} in messages" :sender="sender === user_name" :messages="msg" :online="online"/>
       </div>
        <div class=" rounded-b absolute right-0 left-0 bottom-0">
            <div class="flex border-t-2 items-center justify-between w-full p-3 bg-slate-100">
                <button>
                    <svg xmlns="http://www.w3.org/2000/svg" class="w-5 h-5  text-blue-500" fill="none" viewBox="0 0 24 24"
                    stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                        d="M15.172 7l-6.586 6.586a2 2 0 102.828 2.828l6.414-6.586a4 4 0 00-5.656-5.656l-6.415 6.585a6 6 0 108.486 8.486L20.5 13" />
                    </svg>
                </button>
                <input type="text" placeholder="Message"
                class="block w-full py-2 pl-4 mx-3 bg-gray-100 rounded-full outline-none focus:text-gray-700"
                name="message" required />
                <button type="submit">
                    <svg class="w-5 h-5  text-blue-500 origin-center transform rotate-90" xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20" fill="currentColor">
                        <path
                        d="M10.894 2.553a1 1 0 00-1.788 0l-7 14a1 1 0 001.169 1.409l5-1.429A1 1 0 009 15.571V11a1 1 0 112 0v4.571a1 1 0 00.725.962l5 1.428a1 1 0 001.17-1.408l-7-14z" />
                    </svg>
                </button>
            </div>
        </div>
    </div>
</template>


<script setup>
import { XIcon } from '@heroicons/vue/solid';
import { ref } from 'vue';
import Messages from './Messages.vue';

// setting user_name to current loggged in user
const props = defineProps(['chatUser'])

const sender = ref(props.chatUser.user_name)


const emit = defineEmits(['closeChat'])



const closeChat = () => {
    emit('closeChat','close')
}




const messages = [
    {
        "user_name": "August King",
        "range": "sometime to measure here",
        "online": true,
        "msg": "Hey, I'm doing really well thank you and how are you doing ?"
    },
    {
        "user_name": "The Other Guy",
        "range": "sometime to measure here",
        "online": true,
        "msg": "Yeag baby !!"
    },
    {
        "user_name": "August King",
        "range": "sometime to measure here",
        "online": true,
        "msg": "Dam that sucks man whats the news with you buying a house I hear ?"
    },
       {
        "user_name": "The Other Guy",
        "range": "sometime to measure here",
        "online": true,
        "msg": "Hey, how are you doing ?"
    },
    {
        "user_name": "The Other Guy",
        "range": "sometime to measure here",
        "online": true,
        "msg": "I'am also doing well man, been real busy at work this week tho."
    },
     {
        "user_name": "The Other Guy",
        "range": "sometime to measure here",
        "online": true,
        "msg": "I'am also doing well man, been real busy at work this week tho."
    },
     {
        "user_name": "The Other Guy",
        "range": "sometime to measure here",
        "online": true,
        "msg": "I'am also doing well man, been real busy at work this week tho."
    },
     {
        "user_name": "The Other Guy",
        "range": "sometime to measure here",
        "online": true,
        "msg": "I'am also doing well man, been real busy at work this week tho."
    },
     {
        "user_name": "The Other Guy",
        "range": "sometime to measure here",
        "online": true,
        "msg": "I'am also doing well man, been real busy at work this week tho."
    },
    {
        "user_name": "The Other Guy",
        "range": "sometime to measure here",
        "online": true,
        "msg": "Yea boi!! I get the keys next week."
  }
]
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Karla&display=swap');

.user-header{
   font-family: 'Karla', sans-serif;
}




</style>

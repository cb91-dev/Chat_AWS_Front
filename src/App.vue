<script setup>
import Admin from "./components/Admin.vue";
import Main from "./components/Main.vue";
import { reactive,onMounted } from 'vue'


onMounted(() => {
  const token = localStorage.getItem('JWT')
    if(token){
        auth.LoggedIn = true
        userProfile()
    }else {
        auth.LoggedIn = false
    }
})


// handling logged in user state
const auth = reactive({
   LoggedIn: false,
})


const controller = (event) =>{    
    if(event === true){
        auth.LoggedIn = true
        userProfile()
    }else {
        auth.LoggedIn = false
    }
}
const userProfile = () => {
    const token = localStorage.getItem('JWT')

//     const url = "http://127.0.0.1:8000/profile";
//     const options = {
//     method: "GET",
//     headers: {
//         Accept: "application/json",
//         "Content-Type": "application/json;charset=UTF-8",
//     },
// };
// fetch(url, options)
//   .then((response) => response.json())
//   .then((data) => {
//     if(data.status_code == 200){
//       localStorage.setItem("JWT", data.headers);
//       emit('response',true)
//       return
//     }
//     if(data.status_code == 404){
//       // not a register user
//       error.value = data.detail
//       return 
//     }
//      if(data.status_code == 422){
//       // trying to catch werid error
//       error.value = 'somthing has gone wrong'
//       return 
//     }
//   }).catch((error) => { console.error('Error:', error)
//   });
}
</script>

<template>
    <div >
        <Main class="box" v-if="auth.LoggedIn" @controller=controller />
        <Admin class="box" v-else @controller=controller /> 
    </div>
</template>

<style>
.box{
box-sizing: border-box;
}
</style>

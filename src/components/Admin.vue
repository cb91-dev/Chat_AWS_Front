<script setup>
import Login from './Login.vue';
import Register from './Register.vue';
import { ref, reactive } from 'vue';



const emit = defineEmits(['controller'])

// Switch between login and register
const form_control = reactive({
   Login: true,
   Register:false,
})



const response = (event) => {
    if(event == true){
        emit("controller" ,true)
    }else {
        emit("controller",false)
    }
}

// Switch between login and register
const controller = (event) => {
    console.log('here')
    if (event == 'register'){
    form_control.Login = !form_control.Login
    form_control.Register = !form_control.Register
    }else {
    form_control.Login = !form_control.Login
    form_control.Register = !form_control.Register
    }
}

</script>

<template>

<Login v-if="form_control.Login" @response="response" @form_switch="controller"/>

<Register v-else @response="response" @form_switch="controller"/>


</template>
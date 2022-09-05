<template>
        <div class="p-2">
            <div class="flex flex-col">
                    <div class="flex user-msgs" :class="props.sender ? ' bg-blue-400 rounded p-1  text-white m-1 mr-32 md:mr-96 max-w-max' : ' self-end max-w-max ml-32 md:ml-96 m1 bg-green-400 rounded p-1 text-white '">
                    {{props.messages}}
                    </div>           
            </div>
        </div>
</template>



<script setup>


const props = defineProps(['messages','sender',"online"])


console.log(props.messages)
console.log(props.sender)
</script>


<style>


@import url('https://fonts.googleapis.com/css2?family=Karla&display=swap');
.user-msgs{
   font-family: 'Karla', sans-serif;
}
</style>
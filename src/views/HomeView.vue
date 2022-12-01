
<template>
  <main>


    <div class=" bg-slate-700 dark:bg-white">
    
      <span class=" dark:text-">
        {{ isDark ? "Dark" : "Light" }} Mode

      </span>
      <button @click="toggleDark()">Togle</button>
      <SingelTodoVue    />


    </div>


   
 
  </main>
</template>


<script setup>
import { useDark, useToggle } from "@vueuse/core"
import SingelTodoVue from '../components/SingelTodo.vue';


const isDark = useDark();
const toggleDark = useToggle(isDark);
console.log(isDark.value);




</script>

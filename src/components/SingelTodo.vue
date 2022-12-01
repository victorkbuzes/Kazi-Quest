
<template>
  <div class="h-screen flex flex-col justify-center items-center  ">
    <form @submit.prevent="addTodo" class="">
    
      <!-- <input v-model="newTodo"> -->
      <input v-model="newTodo" class="shadow  border rounded  py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline" id="username" type="text" placeholder="todo">

   
      <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
        Add Todo
      </button>
    </form>
    <ul class=" text-2xl md:text-2xl">
      <li v-for="todo in filteredProjects" :key="todo.id" class=" p-4">
      <input class=" w-6 h-6  rounded-full" type="radio"  v-model="todo.complete">
      <span  :class="{ done: todo.complete }">{{ todo.text }}</span>
      
    
      <span @click="removeTodo(todo)" >X</span>
      </li>
    </ul>
    <button @click="hideCompleted = !hideCompleted">
      {{ hideCompleted ? 'Show all' : 'Clear completed ' }}
    </button>

    <FilterNavVue @filterChange="current = $event" :current="current"  />

  </div>
  

</template>

<script setup>
import { ref, computed } from 'vue'

import FilterNavVue from './FilterNav.vue';

let id = 0

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref([
  { id: id++, text: 'Jog Around the park', complete: true },
  { id: id++, text: '10 minutes meditation', complete: true },
  { id: id++, text: 'Read for 1 hour', complete: false },
  { id: id++, text: 'Pick up groceries', complete: false },
  { id: id++, text: 'Complete todo app on frontend mentor', complete: false }
])
const current = ref('all')
// const todosLength = todos.length
// const remaingTodos = todos.filter((todo) => !todo.complete).length

// const filteredTodos = computed(() => {
//   return hideCompleted.value
//     ? todos.value.filter((t) => !t.complete)
//     : todos.value
// })

const filteredProjects = computed(() => {
  if (current.value === 'completed') {
    return todos.value.filter(todo => todo.complete)
  }
  if (current.value === 'ongoing') {
    return todos.value.filter(todo => !todo.complete)
  }
  return hideCompleted.value
    ? todos.value.filter((t) => !t.complete)
    : todos.value

})

const starDrag = (event, item) => {
  console.log(item);
  event.dataTransfer.dropEffect = 'move'
  event.dataTransfer.effectAllowed = 'move'
  event.dataTransfer.setData('itemID', item.id)

}

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, complete: false })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>


<style>
.done {
  text-decoration: line-through;
}
</style>
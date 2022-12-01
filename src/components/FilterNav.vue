<template>
    <nav class="filter-nav ">
        <button  class=""
        @click="updateFilter('all')"
        :class="{ active: current === 'all' }"
        >All</button>
     
        <button 
        @click="updateFilter('ongoing')"
        :class="{ active: current === 'ongoing' }"
        >Acitve</button>
        <button 
        @click="updateFilter('completed')"
        :class="{ active: current === 'completed' }"
        >Completed</button>

    </nav>
</template>

<script setup>
const emit = defineEmits('filterChange')
const props = defineProps(['current'])
function updateFilter(by) {
    emit('filterChange', by)
    
}
</script>

<style  scoped>
.filter-nav button{
    background: none;
    border: none;
    color: #bbb;
    outline: none;
    font-size: 12px;
    margin-right: 10px;
    letter-spacing: 1px;
    cursor: pointer;
}
.filter-nav button.active{
    color: #555;
}
</style>
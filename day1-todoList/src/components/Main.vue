<script setup lang="ts">
  import TodoList from './TodoList.vue';
  import Menu from './Menu.vue';
  import {ref} from 'vue';

  defineProps<{ msg: string }>()
  let page = ref('today');
  
  function changeComponent(newPage) {
    if(newPage) {
      page.value = newPage;
    }
  }
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="container">
    <Menu :changeComponent="changeComponent" :page="page"/>
    <TodoList title="Today's Todos" v-if="page === 'today'" :page="page"/>
    <TodoList title="Scheduled Todos" v-if="page === 'scheduled'" :page="page"/>
    <TodoList title="Completed Todos" v-if="page === 'completed'" :page="page"/>
  </div>

</template>

<style scoped>
.container {
  min-width: 1000px;
  max-width: 1300px;
  width: 70vw;
  height: 70vh;
  display: flex;
  border-radius: 15px;
  overflow: hidden;
  box-shadow: 0 0 5px rgba(0,0,0,0.2)
}

</style>

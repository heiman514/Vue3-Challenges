<script setup lang="ts">
import Card from './components/Card.vue';
import { onMounted, reactive } from 'vue';

const data = reactive([]);

function fetchData() {
  fetch("http://localhost:3000/day4")
  .then(response => response.json())
  .then(json => data.values = json);
}

onMounted(()=> {
  fetchData();
});

</script>

<template>
  <div class="cardContainer" v-if="data.values.length > 0" >
    <Card v-for="story in data.values" :story="story"/>
  </div>
</template>

<style scoped>
.cardContainer {
  display: flex;
  flex-direction: column;
  justify-content: center;
  gap: 15px;
  align-items: center;
  width: 100%;
  margin: 50px 0;
  min-height: calc(100vh - 100px);
}

</style>

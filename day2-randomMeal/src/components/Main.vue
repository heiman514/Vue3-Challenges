<script setup lang="ts">
import MealDetail from './MealDetail.vue'

</script>

<template>
  <div id="container">
      <h1>Feeling hungry?</h1>
      <h2>Get a random meal by clicking below</h2>
      <MealDetail />
  </div>


</template>

<style scoped>
#container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
}
</style>

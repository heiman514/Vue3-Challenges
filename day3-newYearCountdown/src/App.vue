<script lang="ts" setup>
  import { ref, onMounted } from 'vue';
  
  const timerDay = ref("");
  const timerHours = ref("");
  const timerMinutes = ref("");
  const timerSeconds = ref("");
  const displayYear = ref("");

  function updateTimer() {
    const date:any = new Date();
    const year = date.getFullYear();
    displayYear.value = `${year + 1}`
    
    const yearEnd:any = new Date(`${year}-12-31 23:59:59`);

    const timer = yearEnd - date;
    timerDay.value = `${Math.floor(timer/1000/60/60/24)}`;

    const hours = Math.floor(timer/1000/60/60) % 24;
    timerHours.value = `${hours !== 0 && hours < 10 ? '0' + hours : hours}`;

    const minutes = Math.floor(timer/1000/60) % 60;
    timerMinutes.value = `${minutes !== 0 && minutes < 10 ? '0' + minutes : minutes}`;
    
    const seconds = Math.floor(timer/1000) % 60;    
    timerSeconds.value = `${seconds !== 0 && seconds < 10 ? '0' + seconds : seconds}`;
  }

  onMounted(()=>{
    updateTimer();
    setInterval(updateTimer, 1000);
  });

</script>

<template>
  <div class="container">
    <h1>New Year {{ displayYear }} is Coming!</h1>
    <div class="counter">
      <span>{{ timerDay }}</span>
      <span>{{ timerHours }}</span>
      <span>{{ timerMinutes }}</span>
      <span>{{ timerSeconds }}</span>
    </div>
    <div class="label">
      <span>days</span>
      <span>hours</span>
      <span>minutes</span>
      <span>seconds</span>
    </div>
  </div>
</template>

<style scoped>
.container {
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  color: #fff;
}

.counter {
  width: 30rem;
  display: flex;
  text-align: center;
  font-size: 2rem;
  margin-top: 3rem;
}

.label {
  width: 30rem;
  display: flex;
  text-align: center;
  color: #ddd;
  font-size: 1rem;
}

span {
  width: 25%;
}

@keyframes fall {
	to {
		transform: translateY(105vh);
	}
}

body {
  overflow: hidden;
}

</style>

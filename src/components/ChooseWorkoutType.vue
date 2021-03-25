<template>
  <div class="main small-container">
      <div class="main-title">
        <h3>Please choose the type of workout you would like to register</h3>
      </div>
      <div class="buttons">
        <button class="time-distance-button" @click="$emit('time-distance:button')">Time & Distance</button>
        <button class="sets-reps-button" @click="$emit('sets-reps:button')">Sets & Reps</button>
      </div>
  </div>
</template>

<script>
export default {
    name: 'ChooseWorkoutType'
}
</script>

<style scoped>
  .main {
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  .time-distance-button {
    margin-right: 5px;
  }
  .sets-reps-button {
    margin-left: 5px;
  }
</style>
<template>
  <div class="header">
      <h1 class="title" @click="$emit('title:click')">Fitness Tracker</h1>
      <p class="past-exercises" @click="$emit('past:click')">Past Exercises</p>
  </div>
</template>

<script>
export default {
    name: 'HeaderComponent'
}
</script>

<style scoped>
    .header {
        width: 100%;
        height: 100px;
        background-color: lightseagreen;
        display: flex;
        align-items: center;
        justify-content: space-between;
    }
    .title {
        margin-left: 30px;
        cursor: pointer;
    }
    .title:hover {
        color: white;
    }
    .past-exercises {
        cursor: pointer;
        margin-bottom: -1px;
        margin-right: 30px;
    }
    .past-exercises:hover {
        color: white;
    }
</style>
<template>
  <div class="small-container">
      <table>
          <thead>
              <tr>
                  <td>Name</td>
                  <td>Duration</td>
                  <td>Date</td>
              </tr>
          </thead>
          <tbody>
              <tr v-for="workout in savedWorkouts" :key="workout.id">
                  <td>{{ workout.name }}</td>
                  <td>{{ workout.duration.hours }}:{{ workout.duration.minutes }}:{{ workout.duration.seconds }}</td>
                  <td>{{ workout.date }}</td>
              </tr>
          </tbody>
      </table>
  </div>
</template>

<script>
export default {
    name: 'PastExercises',
    props: {
        savedWorkouts: Array,
    }
}
</script>

<style>

</style>
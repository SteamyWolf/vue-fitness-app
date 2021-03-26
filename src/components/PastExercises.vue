<template>
  <div class="small-container">
      <table>
          <thead>
              <tr>
                  
                  <td><b>Name</b></td>
                  <td><b>Duration</b></td>
                  <td><b>Date</b></td>
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
      <table>
          <thead>
              <tr>
                  <td><b>Name</b></td>
                  <td><b>Sets</b></td>
                  <td><b>Reps</b></td>
                  <td><b>Weight</b></td>
                  <td><b>Date</b></td>
              </tr>
          </thead>
          <tbody>
              <tr v-for="workout in savedRepsWorkouts" :key="workout.id">
                  <td>{{ workout.name }}</td>
                  <td>
                      <div v-for="set in workout.sets" :key="set.id">
                        {{ set }}
                      </div>
                  </td>
                  <td>
                      <div v-for="rep in workout.reps" :key="rep.id">
                        {{ rep }}
                      </div>
                  </td>
                  <td>
                      <div v-for="heav in workout.weight" :key="heav.id">
                        {{ heav }}
                      </div>
                  </td>
                  <td>
                      {{ workout.date }}
                  </td>
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
        savedRepsWorkouts: Array
    }
}
</script>

<style>

</style>
<template>
  <div class="small-container">
      <form @submit.prevent="handleSubmit()">
          <label for="workout-name">Workout Type <i class="red">(required)</i></label>
          <input id="workout-name" type="text" v-model="workoutName" :class="{'has-error': workoutName === '' && submitClicked, 'is-success': submitClicked && workoutName.length > 0}" />
          <!-- <label for="sets">Sets</label>
          <input type="number" id="sets" />
          <label for="reps">Reps</label>
          <input type="number" id="reps" />
          <label for="weight">Weight</label>
          <button type="submit">Submit</button> -->
          <div class="save-success" v-if="saved">Your workout has been saved successfully!</div>
      </form>
      <table>
          <thead>
              <tr>
                  <td>Workout Type</td>
                  <td>Duration</td>
                  <td>Actions</td>
              </tr>
          </thead>
          <!-- <tbody v-if="timeWorkouts.length > 0">
              <tr v-for="workout in timeWorkouts" :key="workout.id">
                  <td>{{ workout.name }}</td>
                  <td>{{ workout.duration.hours }}:{{ workout.duration.minutes }}:{{ workout.duration.seconds }}</td>
                  <td>
                      <button class="accent-button" v-if="!workout.booleans.running" @click="handleStart(workout)">Start</button>
                      <button v-if="workout.booleans.running" @click="handleStop(workout)">Stop</button>
                      <button v-if="!workout.booleans.running" @click="handleSave(workout)">Save</button>
                      <button class="muted-button" @click="handleDelete(workout)">Delete</button>
                  </td>
              </tr>
          </tbody> -->
      </table>
  </div>
</template>

<script>
export default {
    name: 'SetsReps',
    props: {
        repsWorkouts: Array,
    },
    data() {
        return {
            workoutName: '',
            submitClicked: false,
            saved: false
        }
    },
    methods: {
        handleSubmit() {
            this.submitClicked = true;
        }
    }
}
</script>

<style>

</style>
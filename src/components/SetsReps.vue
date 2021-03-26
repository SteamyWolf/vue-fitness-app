<template>
  <div class="medium-container">
      <form @submit.prevent="handleSubmit()">
          <label for="workout-name">Workout Type <i class="red">(required)</i></label>
          <input id="workout-name" type="text" v-model="workoutName" :class="{'has-error': workoutName === '' && submitClicked, 'is-success': submitClicked && workoutName.length > 0}" />
          <button type="submit">Create Workout</button>
          <div class="save-success" v-if="saved">Your workout has been saved successfully!</div>
      </form>
      <table>
          <thead>
              <tr>
                  <td>Workout Type</td>
                  <td>Sets</td>
                  <td>Reps</td>
                  <td>Weight</td>
                  <td>Edit</td>
              </tr>
          </thead>
          <tbody>
              <tr v-for="repsWorkout in repsWorkouts" :key="repsWorkout.id">
                <td>{{ repsWorkout.name }}</td>
                <td>
                    <input v-for="(row, index) in repsWorkout.rows" :key="row.id" type="number" v-model="repsWorkout.sets[index]" :class="{'has-error': repsWorkout.recheck === true}" />
                </td>
                <td>
                    <input v-for="(row, index) in repsWorkout.rows" :key="row.id" type="number" v-model="repsWorkout.reps[index]" />
                </td>
                <td>
                    <input v-for="(row, index) in repsWorkout.rows" :key="row.id" type="number" v-model="repsWorkout.weight[index]" />
                </td>
                <td>
                    <button class="accent-button full-button" @click="handleAddSet(repsWorkout)">Add Set</button>
                    <button class="full-button" @click="handleSaveInfo(repsWorkout)">Save Info</button>
                    <button class="full-button muted-button" @click="handleDelete(repsWorkout)">Delete</button>
                </td>
              </tr>
          </tbody>
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
            saved: false,
            recheck: false
        }
    },
    methods: {
        handleSubmit() {
            this.submitClicked = true;
            if (!this.workoutName) {
                return;
            }
            this.repsWorkouts.push({
                name: this.workoutName,
                rows: 1,
                sets: [],
                reps: [],
                weight: [],
            })
            this.workoutName = '';
            this.submitClicked = false;
        },
        handleAddSet(workout) {
           workout.rows += 1;
        },
        handleSaveInfo(workout) {
            console.log(workout)
            this.recheck = false;
            console.log('made it here')
            if (workout.sets.length < 1 || workout.reps.length < 1 || workout.weight.length < 1) {
                this.recheck = true;
                console.log('inside if')
                return;
            }
            console.log('passed if check')
            let date = new Date().toString().split(' ')
            let combinedDate = `${date[0]} ${date[1]} ${date[2]} ${date[3]}`
            workout.date = combinedDate
            this.saved = true;
            setTimeout(() => {
                this.saved = false;
            }, 5000)
            this.$emit('saveSets:info', workout)
        },
        handleDelete(workout) {
            let index = this.repsWorkouts.findIndex(obj => obj === workout)
            this.repsWorkouts.splice(index, 1);
        }
    }
}
</script>

<style>
   
</style>
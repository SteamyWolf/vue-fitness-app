<template>
  <div class="small-container">
      <form @submit.prevent="handleSubmit()">
          <label for="workout-name">Workout Type <i class="red">(required)</i></label>
          <input id="workout-name" type="text" v-model="workoutName" :class="{'has-error': workoutName === '' && submitClicked, 'is-success': submitClicked && workoutName.length > 0}" />
          <button type="submit">Submit</button>
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
          <tbody v-if="timeWorkouts.length > 0">
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
          </tbody>
      </table>
  </div>
</template>

<script>
export default {
    name: 'TimeDistance',
    props: {
        timeWorkouts: Array,
    },
    data() {
        return {
            submitClicked: false,
            workoutName: '',
            duration: null,
            saved: false
        }
    },
    methods: {
        handleSubmit() {
            this.submitClicked = true;
            if (!this.workoutName) {
                return;
            }
            this.timeWorkouts.push({
                name: this.workoutName,
                duration: {
                    seconds: 0,
                    minutes: 0,
                    hours: 0
                },
                booleans: {
                    running: false,
                    stop: false
                },
                date: null
            })
            this.workoutName = '';
            this.submitClicked = false;
            // this.$emit('timeWorkout:submit', this.workouts)
        },
        handleStart(workout) {
            workout.booleans.running = true;
            workout.booleans.stop = false;
            setTimeout(() => {
                if (workout.booleans.stop) {
                    console.log('hit stop in interval')
                    return;
                }
                if (workout.duration.seconds >= 59) {
                    workout.duration.seconds = -1;
                    workout.duration.minutes += 1;
                }
                if (workout.duration.minutes >= 59) {
                    workout.duration.minutes = -1;
                    workout.duration.hours += 1;
                }
                workout.duration.seconds += 1;

                this.handleStart(workout)
            }, 1000)
        },
        handleStop(workout) {
            workout.booleans.stop = true;
            workout.booleans.running = false;
        },
        handleSave(workout) {
            this.saved = true;
            setTimeout(() => {
                this.saved = false;
            }, 5000)
            let date = new Date().toString().split(' ')
            let combinedDate = `${date[0]} ${date[1]} ${date[2]} ${date[3]}`
            workout.date = combinedDate
            this.$emit('save:workout', workout);
        },
        handleDelete(workout) {
            let index = this.timeWorkouts.findIndex(obj => obj === workout)
            this.timeWorkouts.splice(index, 1);
        }
    }
}
</script>

<style>
    .red {
        color: crimson;
    }
    .save-success {
        color: green;
    }
</style>
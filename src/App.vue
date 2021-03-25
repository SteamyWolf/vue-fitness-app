<template>
  <div class="main-app">
    <header-component @title:click="handleTitleClick" @past:click="handlePastExercisesClick" />
    <div v-if="!past" class="render-workout-view">
      <div class="main-view" v-if="!chosen">
        <choose-workout-type @time-distance:button="handleTimeDistanceClick" @sets-reps:button="handleSetsRepsClick" />
      </div>
      <div class="workout-chosen-view" v-else>
        <div class="time-distance-comp" v-if="timeDistance">
          <time-distance @save:workout="handleSaveWorkout" :timeWorkouts="timeWorkouts" @timeWorkout:submit="handleTimeWorkoutSubmit" />
        </div>
        <div class="sets-reps-comp" v-if="setsReps">
          <sets-reps :repsWorkouts="repsWorkouts" />
        </div>
      </div>
    </div>
    <div v-if="past">
      <past-exercises :savedWorkouts="savedWorkouts" />
    </div>
  </div>
</template>

<script>
import ChooseWorkoutType from "./components/ChooseWorkoutType.vue";
import HeaderComponent from "./components/Header.vue";
import TimeDistance from "./components/TimeDistance.vue";
import SetsReps from "./components/SetsReps.vue";
import PastExercises from './components/PastExercises.vue';

export default {
  name: "App",
  components: {
    ChooseWorkoutType,
    HeaderComponent,
    TimeDistance,
    SetsReps,
    PastExercises,
  },
  data() {
    return {
      chosen: false,
      past: false,
      timeDistance: false,
      setsReps: false,
      savedWorkouts: [],
      timeWorkouts: [],
      repsWorkouts: []
    };
  },
  methods: {
    handleTitleClick() {
      this.chosen = false;
      this.timeDistance = false;
      this.setsReps = false;
      this.past = false;
    },
    handlePastExercisesClick() {
      this.past = true;
    },
    handleTimeDistanceClick() {
      this.timeDistance = true;
      this.chosen = true;
    },
    handleSetsRepsClick() {
      this.chosen = true;
      this.setsReps = true;
    },
    handleSaveWorkout(workout) {
      console.log(workout)
      this.savedWorkouts.push(workout)
    },
    handleTimeWorkoutSubmit(workouts) {
      this.timeWorkouts = workouts;
    }
  },
};
</script>

<style scoped>
</style>
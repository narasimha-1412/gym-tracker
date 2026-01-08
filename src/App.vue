<script setup>
import { computed, onMounted, ref } from "vue";
import Layout from "./components/layout/Layout.vue";
import Dashboard from "./components/pages/Dashboard.vue";
import Welcome from "./components/pages/Welcome.vue";
import Workout from "./components/pages/Workout.vue";
import { workoutProgram } from "./utils/index.js";

const deafultData = {};
for (let id in workoutProgram) {
  const wData = workoutProgram[id];
  deafultData[id] = {};

  for (let e of wData.workout) {
    deafultData[id][e.name] = "";
  }
}

const selectedPage = ref(1);
const data = ref(deafultData);
const selectedWorkout = ref(-1);

const isWorkoutCompleted = computed(() => {
  const currWorkout = data.value?.[selectedWorkout.value];

  if (!currWorkout) {
    return false;
  }

  const isCompleteCheck = Object.values(currWorkout).every((ex) => !!ex);
  return isCompleteCheck;
});

const firstIncompleteWorkoutIndex = computed(() => {
  const allWorkouts = data.value;

  if (!allWorkouts) return -1;

  for (const [indxe, workout] of Object.entries(allWorkouts)) {
    const isCompleteCheck = Object.values(workout).every((ex) => !!ex);
    if (!isCompleteCheck) {
      return parseInt(indxe);
    }
  }

  return -1;
});

function handleChangeDisplay(idx) {
  selectedPage.value = idx;
}

function handleSelectWorkout(idx) {
  selectedPage.value = 3;
  selectedWorkout.value = idx;
}

function handleSaveWorkout() {
  localStorage.setItem("workouts", JSON.stringify(data.value));

  selectedPage.value = 2;

  selectedWorkout.value = -1;
}

function handleResetWorkout() {
  selectedPage.value = 2;
  selectedWorkout.value = -1;
  data.value = deafultData;
  localStorage.removeItem("workouts");
}

onMounted(() => {
  const savedData = localStorage.getItem("workouts");
  if (savedData) {
    data.value = JSON.parse(savedData);
    selectedPage.value = 2;
  }
});
</script>

<template>
  <Layout>
    <Welcome
      :handleChangeDisplay="handleChangeDisplay"
      v-if="selectedPage === 1"
    />
    <Dashboard
      :firstIncompleteWorkoutIndex="firstIncompleteWorkoutIndex"
      :handleSelectWorkout="handleSelectWorkout"
      :handleResetWorkout="handleResetWorkout"
      v-if="selectedPage === 2"
    />
    <Workout
      :isWorkoutCompleted="isWorkoutCompleted"
      :handleSaveWorkout="handleSaveWorkout"
      :data="data"
      :selectedWorkout="selectedWorkout"
      v-if="workoutProgram?.[selectedWorkout]"
    />
  </Layout>
</template>

<style scoped></style>

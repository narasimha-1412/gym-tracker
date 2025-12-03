<script setup>
import { computed, ref } from "vue";
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
const data = ref();
const selectedWorkout = ref(-1);

const isWorkoutCompleted = computed(() => {
  const currWorkout = data.value?.[selectedWorkout.value];

  if (!currWorkout) returnfalse;

  const isCompleteCheck = Object.values(currWorkout).every((ex) => !ex);
  return isCompleteCheck;
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
</script>

<template>
  <Layout>
    <Welcome
      :handleChangeDisplay="handleChangeDisplay"
      v-if="selectedPage === 1"
    />
    <Dashboard
      :handleSelectWorkout="handleSelectWorkout"
      v-if="selectedPage === 2"
    />
    <Workout
      :data="deafultData"
      :selectedWorkout="selectedWorkout"
      v-if="workoutProgram?.[selectedWorkout]"
    />
  </Layout>
</template>

<style scoped></style>

<script setup>
import { gymHealthFacts } from "@/utils/index.js";
import Grid from "../Grid.vue";

const props = defineProps({ handleSelectWorkout: Function });
const randomNum = Math.floor(Math.random() * gymHealthFacts.length);
</script>

<template>
  <section id="dashboard">
    <div class="card tip-container">
      <h2>Welocme Narasimha</h2>
      <div>
        <p class="tip">
          <strong>Daily tips:</strong><br />
          {{ gymHealthFacts[randomNum] }}
        </p>
      </div>
      <button>Start workout ➡</button>
    </div>
    <Grid v-bind="props" />
  </section>
</template>

<style scoped>
.tip-container,
.tip-container div,
#dashboard {
  display: flex;
}

.tip-container,
#dashboard {
  flex-direction: column;
}

#dashboard {
  gap: 2rem;
}

.tip-container {
  gap: 0.5rem;
}

@media (min-width: 640px) {
  .tip-container {
    gap: 1rem;
  }
}
</style>

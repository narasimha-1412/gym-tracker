<script setup>
const { handleChangeDisplay } = defineProps({
  handleChangeDisplay: Function,
});
</script>

<template>
  <section id="welcome">
    <div class="benefits">
      <h2>Complete this program</h2>
      <div>
        <p>✔ Follow this program</p>
        <p>✔ Get fit</p>
        <p>✔ Learn more about GYM</p>
      </div>
    </div>

    <div>
      <h3>Trainig plan</h3>
      <p>This training follows</p>
      <strong>Bro split</strong>
      <h5><i>Push ➡ Pull ➡ Leg ➡ Repeat</i></h5>
    </div>

    <div class="card challenge">
      <h3>🔥 Your Challenge</h3>
      <p>Complete all the workouts</p>
      <p>Do you agree?</p>
      <button @click="handleChangeDisplay(2)">Begin ➡</button>
    </div>
  </section>
</template>

<style lang="css" scoped>
#welcome,
.benefits,
.challenge {
  display: flex;
  flex-direction: column;
}

#welcome {
  gap: 1.5rem;
}
.benefits {
  gap: 0.5rem;
}
.challenge {
  gap: 0.25rem;
}
@media (min-width: 640px) {
  #welcome {
    gap: 2rem;
    padding: 1rem 0;
  }

  .benefits {
    gap: 1rem;
  }
}
</style>

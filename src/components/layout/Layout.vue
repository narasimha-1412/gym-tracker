<script setup></script>

<template>
  <header class="text-gradient"><h1>Gym Tracker</h1></header>
  <main>
    <slot />
  </main>
  <footer>
    <small>Created by</small>
    <a href="https://www.github.com/jamezmca" target="_blank">
      <img
        alt="pfp"
        src="https://avatars.githubusercontent.com/u/118914535?v=4"
      />
      <p>Narasimha</p>
      <i class="fa-brands fa-github"></i>
    </a>
  </footer>
</template>

<style scoped>
header,
footer,
main {
  padding: 1rem;
  width: 100%;
  max-width: 37.5rem;
  margin: 0 auto;
}

main {
  flex: 1;
}

footer {
  display: flex;
  flex-direction: column;
  gap: 0.5rem;
  align-items: center;
  padding: 2rem 0;
  padding-bottom: 3rem;
}

footer a {
  display: flex;
  align-items: center;
  gap: 0.5rem;
  padding: 0.3rem;
  padding-right: 0.5rem;
  background: var(--background-muted);
  border-radius: 4rem;
  border: 0.0625rem solid transparent;
  transition-duration: 200ms;
  text-decoration: none;
}

footer a:hover {
  border-color: var(--color-link);
}

footer a img {
  max-width: 1.875rem;
  aspect-ratio: 1 / 1;
  border-radius: 100%;
}
</style>

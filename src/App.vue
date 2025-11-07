<script setup lang="ts">
import ChuckList from './components/ChuckList.vue'

type ChuckJoke = { icon_url: string; value: string }

const iconUrl = 'https://assets.chucknorris.host/img/avatar/chuck-norris.png'

const chuck: ChuckJoke[] = [
  { icon_url: iconUrl, value: 'Chuck Norris can skydive into outer space.' },
  { icon_url: iconUrl, value: 'The chief export of Chuck Norris is pain.' },
  {
    icon_url: iconUrl,
    value:
      "Chuck Norris doesn't read books. He stares them down until he gets the information he wants.",
  },
  { icon_url: iconUrl, value: 'Time waits for no man. Unless that man is Chuck Norris.' },
  { icon_url: iconUrl, value: 'If you spell Chuck Norris in Scrabble, you win. Forever.' },
]
</script>

<template>
  <section class="page">
    <header class="header">
      <h1>Chuck Norris Jokes</h1>
      <p class="subtitle">Colección minimalista de chistes</p>
    </header>

    <main>
      <ChuckList :jokes="chuck" />
    </main>
  </section>
</template>

<style scoped>
.page {
  display: flex;
  flex-direction: column;
  gap: 2rem;
  align-items: center;
  /* Ocupa ambas columnas cuando #app usa grid (>=1024px) */
  grid-column: 1 / -1;
}

.header {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  gap: 0.5rem;
}

h1 {
  font-size: 2rem;
  color: var(--color-heading);
}

.subtitle {
  color: var(--color-text);
  opacity: 0.8;
}
</style>

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

import { ref } from 'vue'
const notification = ref<string | null>(null)
let hideTimer: number | null = null

async function handleSelect(joke: ChuckJoke, index: number) {
  const text = joke.value
  try {
    if ('clipboard' in navigator && navigator.clipboard?.writeText) {
      await navigator.clipboard.writeText(text)
    } else {
      const ta = document.createElement('textarea')
      ta.value = text
      document.body.appendChild(ta)
      ta.select()
      document.execCommand('copy')
      document.body.removeChild(ta)
    }
    notification.value = 'Chiste copiado al portapapeles'
  } catch {
    notification.value = 'No se pudo copiar. Intenta manualmente.'
  }
  if (hideTimer) window.clearTimeout(hideTimer)
  hideTimer = window.setTimeout(() => (notification.value = null), 2000)
}
</script>

<template>
  <section class="page">
    <header class="header">
      <h1>Chuck Norris Jokes</h1>
      <p class="subtitle">Colección minimalista de chistes</p>
    </header>

    <main>
      <ChuckList :jokes="chuck" @select="handleSelect" />
      <div v-if="notification" class="toast">{{ notification }}</div>
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

.toast {
  position: fixed;
  left: 50%;
  bottom: 24px;
  transform: translateX(-50%);
  padding: 0.5rem 0.75rem;
  border-radius: 8px;
  background: var(--color-background);
  border: 1px solid var(--color-border);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.08);
  color: var(--color-text);
  z-index: 1000;
}
</style>

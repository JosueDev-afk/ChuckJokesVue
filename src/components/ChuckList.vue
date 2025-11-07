<script setup lang="ts">
type ChuckJoke = { icon_url: string; value: string }

const props = defineProps<{ jokes: ChuckJoke[] }>()

const fallbackSrc = '/favicon.ico'
const onImgError = (e: Event) => {
  const img = e.target as HTMLImageElement
  img.src = fallbackSrc
}
</script>

<template>
  <section class="list">
    <ul>
      <li v-for="(joke, index) in props.jokes" :key="index" class="card">
        <img class="avatar" :src="joke.icon_url" alt="Chuck Norris avatar" @error="onImgError" />
        <p class="text">{{ joke.value }}</p>
      </li>
    </ul>
  </section>
  
</template>

<style scoped>

.list {
  max-width: 900px;
  margin: 0 auto;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
  display: grid;
  grid-template-columns: 1fr;
  gap: 1.25rem;
  justify-items: center;
}

.card {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.75rem;
  padding: 1rem;
  border: 1px solid var(--color-border);
  border-radius: 12px;
  background: var(--color-background-soft);
  transition: transform 0.15s ease, box-shadow 0.15s ease;
  width: 100%;
  max-width: 420px;
}

.card:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.08);
}

.avatar {
  width: 64px;
  height: 64px;
  border-radius: 50%;
  border: 2px solid var(--color-border);
  background: var(--color-background);
  object-fit: cover;
}

.index {
  font-weight: 600;
  color: hsla(160, 100%, 37%, 1);
}

.text {
  color: var(--color-text);
}

@media (min-width: 768px) {
  ul {
    grid-template-columns: 1fr 1fr;
  }

  .avatar {
    width: 72px;
    height: 72px;
  }
}
</style>
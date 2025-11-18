<script setup lang="ts">
type ChuckJoke = { icon_url: string; value: string }

const props = defineProps<{ jokes: ChuckJoke[] }>()

const fallbackSrc = '/favicon.ico'
const onImgError = (e: Event) => {
  const img = e.target as HTMLImageElement
  img.onerror = null
  img.src = fallbackSrc
}
</script>

<template>
  <section class="list" aria-label="Chuck Norris jokes">
    <ul>
      <li v-for="(joke, index) in props.jokes" :key="index" class="card" role="article">
        <figure class="figure">
          <img
            class="avatar"
            :src="joke.icon_url"
            alt="Avatar de Chuck Norris"
            loading="lazy"
            decoding="async"
            @error="onImgError"
          />
          <figcaption class="text">{{ joke.value }}</figcaption>
        </figure>
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
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  place-content: center;
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
  text-align: center;
}

.card:hover {
  transform: translateY(-2px);
  box-shadow: 0 6px 16px rgba(0, 0, 0, 0.08);
}

.figure {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.75rem;
  width: 100%;
}

.avatar {
  width: 72px;
  height: 72px;
  border-radius: 50%;
  border: 2px solid var(--color-border);
  background: var(--color-background);
  object-fit: cover;
}

.text {
  color: var(--color-text);
  line-height: 1.5;
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
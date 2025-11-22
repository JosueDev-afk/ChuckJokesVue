<script setup lang="ts">
type ChuckJoke = { icon_url: string; value: string }

const props = defineProps<{ jokes: ChuckJoke[] }>()

const fallbackSrc = '/favicon.ico'
const onImgError = (e: Event) => {
  const img = e.target as HTMLImageElement
  img.onerror = null
  img.src = fallbackSrc
}

const emit = defineEmits<{
  (e: 'select', joke: ChuckJoke, index: number): void
}>()

const onCardClick = (joke: ChuckJoke, index: number) => emit('select', joke, index)
const onCardKeydown = (event: KeyboardEvent, joke: ChuckJoke, index: number) => {
  if (event.key === 'Enter' || event.key === ' ') {
    event.preventDefault()
    emit('select', joke, index)
  }
}
</script>

<template>
  <section class="list" aria-label="Chuck Norris jokes">
    <TransitionGroup name="list" tag="ul" role="list">
      <li v-for="(joke, index) in props.jokes" :key="joke.value" class="card" role="listitem">
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
    </TransitionGroup>
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

.card.interactive {
  cursor: pointer;
  outline: none;
}

.card.interactive:focus-visible {
  box-shadow: 0 0 0 3px hsla(160, 100%, 37%, 0.35);
  transform: none;
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

/* Transiciones para la lista (TransitionGroup) */
.list-enter-active,
.list-leave-active {
  transition: opacity 250ms ease, transform 250ms ease;
}
.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(8px);
}
/* Movimiento suave cuando cambia el orden */
.list-move {
  transition: transform 250ms ease;
}

@media (prefers-reduced-motion: reduce) {
  .list-enter-active,
  .list-leave-active,
  .list-move {
    transition: none;
  }
}
</style>
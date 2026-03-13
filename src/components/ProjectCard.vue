<template>
  <article class="card" :style="{ '--delay': `${index * 60}ms` }">
    <!-- Thumbnail -->
    <div class="card__thumb" @click="emit('open-modal', project)">
      <img
        :src="thumbnailUrl"
        :alt="project.title"
        class="card__img"
        loading="lazy"
      />
      <div class="card__overlay">
        <div class="card__play">
          <i class="fas fa-play"></i>
        </div>
        <span class="card__watch">Watch Demo</span>
      </div>
    </div>

    <!-- Body -->
    <div class="card__body">
      <h3 class="card__title">{{ project.title }}</h3>
      <p class="card__desc">{{ project.description }}</p>

      <div class="card__tech">
        <span v-for="tech in project.technologies" :key="tech" class="card__badge">
          {{ tech }}
        </span>
      </div>
    </div>

    <!-- Footer -->
    <div class="card__footer">
      <button class="card__btn" @click="emit('open-modal', project)">
        View Project <i class="fas fa-arrow-right"></i>
      </button>
    </div>
  </article>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  project: { type: Object, required: true },
  index:   { type: Number, default: 0 }
})

const emit = defineEmits(['open-modal'])

const thumbnailUrl = computed(() =>
  `https://img.youtube.com/vi/${props.project.videoId}/maxresdefault.jpg`
)
</script>

<style scoped>
.card {
  display: flex;
  flex-direction: column;
  background: var(--bg-2);
  border: 1px solid var(--border);
  border-radius: 14px;
  overflow: hidden;
  transition: border-color 0.25s ease, transform 0.3s ease, box-shadow 0.3s ease;
  animation: card-in 0.55s ease both;
  animation-delay: var(--delay, 0ms);
}

@keyframes card-in {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}

.card:hover {
  border-color: var(--border-md);
  transform: translateY(-5px);
  box-shadow: 0 20px 48px rgba(0, 0, 0, 0.45);
}

/* Thumbnail */
.card__thumb {
  position: relative;
  aspect-ratio: 16 / 9;
  overflow: hidden;
  cursor: pointer;
  background: var(--bg-3);
  flex-shrink: 0;
}

.card__img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.45s ease;
  display: block;
}
.card:hover .card__img { transform: scale(1.04); }

.card__overlay {
  position: absolute;
  inset: 0;
  background: rgba(0, 0, 0, 0.48);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 10px;
  opacity: 0;
  transition: opacity 0.3s ease;
}
.card__thumb:hover .card__overlay { opacity: 1; }

.card__play {
  width: 54px;
  height: 54px;
  border-radius: 50%;
  background: rgba(255, 255, 255, 0.95);
  display: flex;
  align-items: center;
  justify-content: center;
  color: #0a0a0a;
  font-size: 1rem;
  transition: transform 0.25s ease;
  padding-left: 3px;
}
.card__thumb:hover .card__play { transform: scale(1.08); }

.card__watch {
  font-size: 0.75rem;
  font-weight: 600;
  color: rgba(255, 255, 255, 0.85);
  letter-spacing: 0.06em;
  text-transform: uppercase;
}

/* Body */
.card__body {
  padding: 20px 22px 14px;
  flex: 1;
}

.card__title {
  font-size: 1rem;
  font-weight: 700;
  letter-spacing: -0.01em;
  color: var(--text-1);
  margin-bottom: 8px;
  line-height: 1.3;
}

.card__desc {
  font-size: 0.84rem;
  color: var(--text-2);
  line-height: 1.6;
  margin-bottom: 14px;
  display: -webkit-box;
  -webkit-line-clamp: 3;
  -webkit-box-orient: vertical;
  overflow: hidden;
}

.card__tech {
  display: flex;
  flex-wrap: wrap;
  gap: 6px;
}

.card__badge {
  padding: 3px 10px;
  border-radius: 100px;
  border: 1px solid var(--border);
  font-size: 0.7rem;
  font-weight: 500;
  color: var(--text-3);
  background: var(--bg-0);
  font-family: var(--font-mono);
  letter-spacing: 0.03em;
  transition: all 0.2s;
}
.card:hover .card__badge {
  border-color: var(--border-md);
  color: var(--text-2);
}

/* Footer */
.card__footer {
  padding: 14px 22px 20px;
  border-top: 1px solid var(--border);
}

.card__btn {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  font-size: 0.82rem;
  font-weight: 600;
  color: var(--text-2);
  transition: color 0.2s, gap 0.2s;
  letter-spacing: 0.01em;
}
.card__btn:hover {
  color: var(--white);
  gap: 10px;
}
.card__btn i {
  font-size: 0.7rem;
  transition: transform 0.2s;
}
.card__btn:hover i { transform: translateX(2px); }
</style>

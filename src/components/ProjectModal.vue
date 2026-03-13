<template>
  <Teleport to="body">
    <Transition name="modal">
      <div
        v-if="show"
        class="modal-overlay"
        @click.self="emit('close')"
        role="dialog"
        aria-modal="true"
      >
        <div class="modal-panel">
          <!-- Header -->
          <div class="modal-header">
            <div class="modal-header__left">
              <span class="modal-label">Project</span>
              <h2 class="modal-title">{{ project?.title }}</h2>
            </div>
            <button class="modal-close" @click="emit('close')" aria-label="Close modal">
              <i class="fas fa-times"></i>
            </button>
          </div>

          <!-- Content -->
          <div v-if="project" class="modal-body">
            <!-- Video -->
            <div class="modal-video">
              <div class="video-wrap">
                <iframe
                  :src="youtubeEmbedUrl"
                  title="Project demo video"
                  frameborder="0"
                  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                  allowfullscreen
                ></iframe>
              </div>
            </div>

            <!-- Details -->
            <div class="modal-details">
              <div class="detail-block">
                <p class="detail-block__label">About</p>
                <p class="detail-block__text">{{ project.longDescription }}</p>
              </div>

              <div class="detail-block">
                <p class="detail-block__label">Tech Stack</p>
                <div class="modal-tags">
                  <span
                    v-for="tech in project.technologies"
                    :key="tech"
                    class="modal-tag"
                  >{{ tech }}</span>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
import { computed, watch } from 'vue'

const props = defineProps({
  project: { type: Object, default: null },
  show:    { type: Boolean, default: false }
})

const emit = defineEmits(['close'])

const youtubeEmbedUrl = computed(() => {
  if (!props.project?.videoId) return ''
  return `https://www.youtube.com/embed/${props.project.videoId}?autoplay=1&rel=0`
})

watch(() => props.show, (val) => {
  document.body.style.overflow = val ? 'hidden' : ''
})
</script>

<style scoped>
/* Overlay */
.modal-overlay {
  position: fixed;
  inset: 0;
  z-index: 2000;
  background: rgba(0, 0, 0, 0.75);
  backdrop-filter: blur(8px);
  -webkit-backdrop-filter: blur(8px);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

/* Panel */
.modal-panel {
  width: 100%;
  max-width: 880px;
  max-height: 90vh;
  background: var(--bg-2);
  border: 1px solid var(--border-md);
  border-radius: 18px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  box-shadow: 0 32px 80px rgba(0, 0, 0, 0.65);
}

/* Header */
.modal-header {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  padding: 24px 28px 20px;
  border-bottom: 1px solid var(--border);
  flex-shrink: 0;
}
.modal-header__left { display: flex; flex-direction: column; gap: 4px; }
.modal-label {
  font-family: var(--font-mono);
  font-size: 0.66rem;
  font-weight: 500;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--text-3);
}
.modal-title {
  font-size: 1.25rem;
  font-weight: 800;
  letter-spacing: -0.02em;
  color: var(--text-1);
  line-height: 1.2;
}

.modal-close {
  width: 34px;
  height: 34px;
  border-radius: 8px;
  background: var(--bg-3);
  border: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--text-2);
  font-size: 0.85rem;
  transition: all 0.2s;
  flex-shrink: 0;
}
.modal-close:hover {
  background: var(--bg-4);
  border-color: var(--border-md);
  color: var(--white);
}

/* Body */
.modal-body {
  overflow-y: auto;
  flex: 1;
  padding: 24px 28px 28px;
  display: flex;
  flex-direction: column;
  gap: 24px;
}

/* Video */
.modal-video { flex-shrink: 0; }
.video-wrap {
  position: relative;
  width: 100%;
  aspect-ratio: 16 / 9;
  border-radius: 10px;
  overflow: hidden;
  background: var(--bg-0);
  border: 1px solid var(--border);
}
.video-wrap iframe {
  position: absolute;
  inset: 0;
  width: 100%;
  height: 100%;
}

/* Details */
.modal-details {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 20px;
}

.detail-block {
  padding: 20px;
  background: var(--bg-3);
  border: 1px solid var(--border);
  border-radius: 10px;
}
.detail-block__label {
  font-family: var(--font-mono);
  font-size: 0.68rem;
  font-weight: 500;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--text-3);
  margin-bottom: 10px;
}
.detail-block__text {
  font-size: 0.9rem;
  color: var(--text-2);
  line-height: 1.7;
}

.modal-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 7px;
}
.modal-tag {
  padding: 4px 12px;
  border-radius: 100px;
  border: 1px solid var(--border-md);
  font-size: 0.75rem;
  font-weight: 500;
  font-family: var(--font-mono);
  color: var(--text-2);
  background: var(--bg-2);
}

/* Scrollbar inside modal */
.modal-body::-webkit-scrollbar       { width: 4px; }
.modal-body::-webkit-scrollbar-track { background: transparent; }
.modal-body::-webkit-scrollbar-thumb { background: var(--bg-4); border-radius: 2px; }

/* Transition */
.modal-enter-active,
.modal-leave-active {
  transition: opacity 0.25s ease;
}
.modal-enter-active .modal-panel,
.modal-leave-active .modal-panel {
  transition: transform 0.28s ease, opacity 0.25s ease;
}
.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}
.modal-enter-from .modal-panel {
  transform: scale(0.95) translateY(10px);
  opacity: 0;
}
.modal-leave-to .modal-panel {
  transform: scale(0.97) translateY(6px);
  opacity: 0;
}

/* Responsive */
@media (max-width: 640px) {
  .modal-panel       { border-radius: 14px; max-height: 95vh; }
  .modal-header      { padding: 18px 20px 16px; }
  .modal-body        { padding: 18px 20px 22px; }
  .modal-details     { grid-template-columns: 1fr; }
}
</style>

<template>
  <div class="project-card h-100" :style="{ animationDelay: `${index * 0.1}s` }">
    <div class="card bg-dark text-white border-0 shadow-lg h-100">
      <div class="card-img-container position-relative">
        <div class="video-thumbnail" @click="emit('open-modal', project)">
          <img 
            :src="thumbnailUrl" 
            :alt="project.title"
            class="card-img-top"
          />
          <div class="play-overlay">
            <div class="play-button">
              <i class="fas fa-play"></i>
            </div>
          </div>
        </div>
      </div>
      
      <div class="card-body d-flex flex-column">
        <h5 class="card-title fw-bold">{{ project.title }}</h5>
        <p class="card-text flex-grow-1">{{ project.description }}</p>
        
        <div class="tech-stack mb-3">
          <span 
            v-for="tech in project.technologies" 
            :key="tech"
            class="badge tech-badge me-1 mb-1"
          >
            {{ tech }}
          </span>
        </div>
        
        <div class="card-actions">
          <button 
            @click="emit('open-modal', project)"
            class="btn btn-primary btn-sm me-2 mb-2"
          >
            <i class="fas fa-eye me-1"></i>
            View Details
          </button>
        
        </div>
      
      </div>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

// Props
const props = defineProps({
  project: {
    type: Object,
    required: true
  },
  index: {
    type: Number,
    default: 0
  }
})

// Emits
const emit = defineEmits(['open-modal'])

// Computed
const thumbnailUrl = computed(() => {
  return `https://img.youtube.com/vi/${props.project.videoId}/maxresdefault.jpg`
})
</script>

<style scoped>
.project-card {
  opacity: 0;
  transform: translateY(30px);
  transition: all 0.6s ease-out;
}

.project-card.animate-in {
  opacity: 1;
  transform: translateY(0);
}

.card {
  background: rgba(255, 255, 255, 0.1) !important;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1) !important;
  transition: all 0.3s ease;
  overflow: hidden;
}

.card:hover {
  transform: translateY(-10px);
  box-shadow: 0 20px 40px rgba(0, 0, 0, 0.3) !important;
}

.card-img-container {
  overflow: hidden;
  height: 200px;
}

.video-thumbnail {
  position: relative;
  cursor: pointer;
  height: 100%;
}

.card-img-top {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.3s ease;
}

.video-thumbnail:hover .card-img-top {
  transform: scale(1.05);
}

.play-overlay {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: rgba(0, 0, 0, 0.3);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity 0.3s ease;
}

.video-thumbnail:hover .play-overlay {
  opacity: 1;
}

.play-button {
  width: 60px;
  height: 60px;
  background: rgba(255, 255, 255, 0.9);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 20px;
  color: #333;
  transition: all 0.3s ease;
}

.play-button:hover {
  background: white;
  transform: scale(1.1);
}

.tech-badge {
  background: linear-gradient(45deg, #667eea, #764ba2);
  font-size: 0.7rem;
  padding: 4px 8px;
}

.card-actions {
  display: flex;
  flex-wrap: wrap;
  gap: 5px;
}

.btn {
  transition: all 0.3s ease;
}

.btn:hover {
  transform: translateY(-2px);
}

/* Responsive adjustments */
@media (max-width: 768px) {
  .card-img-container {
    height: 180px;
  }
  
  .card-actions {
    flex-direction: column;
  }
  
  .btn {
    width: 100%;
  }
}

@media (max-width: 576px) {
  .card-img-container {
    height: 160px;
  }
  
  .play-button {
    width: 50px;
    height: 50px;
    font-size: 16px;
  }
}
</style>
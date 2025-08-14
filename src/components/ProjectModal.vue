<template>
  <div 
    class="modal fade" 
    :class="{ show: show }"
    :style="{ display: show ? 'block' : 'none' }"
    tabindex="-1"
    @click.self="emit('close')"
  >
    <div class="modal-dialog modal-xl modal-dialog-centered">
      <div class="modal-content bg-dark text-white">
        <div class="modal-header border-secondary">
          <h5 class="modal-title fw-bold">{{ project?.title }}</h5>
          <button 
            type="button" 
            class="btn-close btn-close-white" 
            @click="emit('close')"
          ></button>
        </div>
        
        <div class="modal-body">
          <div v-if="project" class="row">
            <!-- Video Player -->
            <div class="col-lg-8 mb-4">
              <div class="video-container">
                <iframe
                  :src="youtubeEmbedUrl"
                  class="w-100"
                  height="400"
                  frameborder="0"
                  allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture"
                  allowfullscreen
                ></iframe>
              </div>
            </div>
            
            <!-- Project Details -->
            <div class="col-lg-4">
              <div class="project-details">
                <h6 class="fw-bold mb-3">
                  <i class="fas fa-info-circle me-2"></i>
                  Project Details
                </h6>
                
                <div class="detail-section mb-4">
                  <h6 class="text-primary mb-2">Description</h6>
                  <p class="text-light">{{ project.longDescription }}</p>
                </div>
                
                <div class="detail-section mb-4">
                  <h6 class="text-primary mb-2">Technologies Used</h6>
                  <div class="tech-stack">
                    <span 
                      v-for="tech in project.technologies" 
                      :key="tech"
                      class="badge tech-badge me-2 mb-2"
                    >
                      {{ tech }}
                    </span>
                  </div>
                </div>
                <!--
                <div class="action-buttons">
                  <a 
                    :href="project.githubUrl" 
                    target="_blank" 
                    class="btn btn-outline-light btn-sm me-2 mb-2"
                  >
                    <i class="fab fa-github me-2"></i>
                    View Source Code
                  </a>
                  <a 
                    :href="project.liveUrl" 
                    target="_blank" 
                    class="btn btn-primary btn-sm mb-2"
                  >
                    <i class="fas fa-external-link-alt me-2"></i>
                    Live Demo
                  </a>
                </div>
              -->
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  
  <!-- Modal Backdrop -->
  <div 
    v-if="show"
    class="modal-backdrop fade show"
    @click="emit('close')"
  ></div>
</template>

<script setup>
import { computed, watch, nextTick } from 'vue'

// Props
const props = defineProps({
  project: {
    type: Object,
    default: null
  },
  show: {
    type: Boolean,
    default: false
  }
})

// Emits
const emit = defineEmits(['close'])

// Computed
const youtubeEmbedUrl = computed(() => {
  if (!props.project?.videoId) return ''
  return `https://www.youtube.com/embed/${props.project.videoId}?autoplay=1&rel=0`
})

// Watchers
watch(() => props.show, (newVal) => {
  nextTick(() => {
    if (newVal) {
      document.body.style.overflow = 'hidden'
    } else {
      document.body.style.overflow = ''
    }
  })
})
</script>

<style scoped>
.modal {
  z-index: 1055;
}

.modal-backdrop {
  z-index: 1050;
}

.modal-content {
  background: rgba(33, 37, 41, 0.95) !important;
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.video-container {
  position: relative;
  border-radius: 10px;
  overflow: hidden;
  box-shadow: 0 10px 30px rgba(0, 0, 0, 0.3);
}

.video-container iframe {
  border-radius: 10px;
}

.project-details {
  height: 100%;
  padding: 20px;
  background: rgba(255, 255, 255, 0.05);
  border-radius: 10px;
  border: 1px solid rgba(255, 255, 255, 0.1);
}

.detail-section {
  border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  padding-bottom: 15px;
}

.detail-section:last-child {
  border-bottom: none;
  padding-bottom: 0;
}

.tech-badge {
  background: linear-gradient(45deg, #667eea, #764ba2);
  font-size: 0.75rem;
  padding: 5px 10px;
}

.action-buttons .btn {
  transition: all 0.3s ease;
}

.action-buttons .btn:hover {
  transform: translateY(-2px);
}

/* Responsive Design */
@media (max-width: 992px) {
  .modal-dialog {
    max-width: 90%;
  }
  
  .video-container iframe {
    height: 300px;
  }
}

@media (max-width: 768px) {
  .modal-dialog {
    max-width: 95%;
    margin: 10px;
  }
  
  .video-container iframe {
    height: 250px;
  }
  
  .project-details {
    margin-top: 20px;
  }
}

@media (max-width: 576px) {
  .video-container iframe {
    height: 200px;
  }
  
  .action-buttons {
    display: flex;
    flex-direction: column;
  }
  
  .action-buttons .btn {
    width: 100%;
    margin: 5px 0;
  }
}
</style>
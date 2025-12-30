<template>
  <div class="portfolio-wrapper">
    <!-- Animated Background -->
    <div class="bg-animation">
      <div class="blob blob-1"></div>
      <div class="blob blob-2"></div>
      <div class="blob blob-3"></div>
    </div>
    <!-- Header Section -->
    <header class="hero-section text-center text-white py-5">
      <div class="container">
        <div class="row justify-content-center">
          <div class="col-lg-8">
            <h1 class="display-4 fw-bold mb-3 animate-fade-up">
              Hi! I'm Kim David Ritardo
            </h1>
            <p class="lead mb-4 animate-fade-up-delay">
              Creating digital experiences with modern technologies
            </p>
            <div class="scroll-indicator animate-bounce">
              <i class="fas fa-chevron-down"></i>
            </div>
          </div>
        </div>
      </div>
    </header>

    <!-- Projects Section -->
    <section class="projects-section py-5">
      <div class="container">
        <div class="row">
          <div class="col-12">
            <h2 class="text-center mb-5 text-white fw-bold">My Projects</h2>
            
            <!-- Tab Navigation -->
            <ul class="nav nav-pills nav-fill mb-4" id="projectTabs" role="tablist">
              <li class="nav-item" role="presentation">
                <button 
                  class="nav-link active custom-tab" 
                  id="latest-tab" 
                  data-bs-toggle="pill" 
                  data-bs-target="#latest" 
                  type="button" 
                  role="tab"
                  @click="activeTab = 'latest'"
                >
                  <i class="fas fa-rocket me-2"></i>
                  Latest Technologies
                </button>
              </li>
              <li class="nav-item" role="presentation">
                <button 
                  class="nav-link custom-tab" 
                  id="vanilla-tab" 
                  data-bs-toggle="pill" 
                  data-bs-target="#vanilla" 
                  type="button" 
                  role="tab"
                  @click="activeTab = 'vanilla'"
                >
                  <i class="fas fa-code me-2"></i>
                  Vanilla Projects
                </button>
              </li>
            </ul>

            <!-- Tab Content -->
            <div class="tab-content" id="projectTabsContent">
              <!-- Latest Technologies Tab -->
              <div 
                class="tab-pane fade show active" 
                id="latest" 
                role="tabpanel"
              >
                <div class="row g-4">
                  <div 
                    v-for="(project, index) in latestProjects" 
                    :key="project.id"
                    class="col-lg-4 col-md-6"
                  >
                    <div class="project-wrapper h-100" :style="{ animationDelay: `${index * 100}ms` }">
                      <ProjectCard 
                        :project="project" 
                        :index="index"
                        @open-modal="openModal"
                      />
                    </div>
                  </div>
                </div>
              </div>

              <!-- Vanilla Projects Tab -->
              <div 
                class="tab-pane fade" 
                id="vanilla" 
                role="tabpanel"
              >
                <div class="row g-4">
                  <div 
                    v-for="(project, index) in vanillaProjects" 
                    :key="project.id"
                    class="col-lg-4 col-md-6"
                  >
                    <div class="project-wrapper h-100" :style="{ animationDelay: `${index * 100}ms` }">
                      <ProjectCard 
                        :project="project" 
                        :index="index"
                        @open-modal="openModal"
                      />
                    </div>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Project Modal -->
    <ProjectModal 
      :project="selectedProject"
      :show="showModal"
      @close="closeModal"
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import ProjectCard from './ProjectCard.vue'
import ProjectModal from './ProjectModal.vue'

// Reactive data
const activeTab = ref('latest')
const showModal = ref(false)
const selectedProject = ref(null)

// Sample project data - replace with your actual projects
const latestProjects = ref([
  {
    id: 1,
    title: 'LU Chats',
    description: 'This project is a fully responsive web application designed to provide a simple communication between students and faculty at Laguna University.',
    technologies: ['PHP','Laravel', 'Bootstrap 4', 'JavaScript'],
    videoId: 'CRYmVVQ9R5Q', // Replace with your YouTube video ID
    githubUrl: 'https://github.com/yourusername/vue-dashboard',
    liveUrl: 'https://yourvuedashboard.com',
    longDescription: 'This project is a fully responsive web application designed to provide a simple communication between students and faculty at Laguna University.'
  },
  {
    id: 2,
    title: 'LU Supply Office System',
    description: 'A web inventory system Made with PHP Laravel 10...',
    technologies: ['PHP','Laravel', 'Bootstrap 4', 'JavaScript'],
    videoId: 'kMFIr-V82aY', // Replace with your YouTube video ID
    githubUrl: 'https://github.com/yourusername/social-app',
    liveUrl: 'https://yoursocialapp.com',
    longDescription: 'A web inventory system Made with PHP Laravel 10...'
  }

])

const vanillaProjects = ref([
  {
    id: 5,
    title: 'e-Commerce Project',
    description: 'A simple e-commerce project for internship...',
    technologies: ['PHP','Codeigniter', 'Bootstrap 4', 'JavaScript'],
    videoId: 'h2QoEEtr_Qw', // Replace with your YouTube video ID
    githubUrl: 'https://github.com/yourusername/js-calculator',
    liveUrl: 'https://yourjscalculator.com',
    longDescription: 'This project is created during my internship at Village88 inc a simple e-commerce site created using codeigniter.'
  },
  {
    id: 6,
    title: 'Crime Monitoring and Analysis',
    description: 'A web-based crime monitoring,reporting and analysis...',
    technologies: ['PHP', 'Bootstrap 4', 'JavaScript','SMS API'],
    videoId: 'IuDbhb7Q0Pk', // Replace with your YouTube video ID
    githubUrl: 'https://github.com/yourusername/css-gallery',
    liveUrl: 'https://yourcssgallery.com',
    longDescription: 'A web-based crime monitoring,reporting and analysis...'
  },
  {
    id: 7,
    title: 'Pharmabot',
    description: 'A simple voice recognition bot made using C#...',
    technologies: ['C#.NET', 'Voice Recognition','External Microphone'],
    videoId: 'MbE1aleSOZU', // Replace with your YouTube video ID
    githubUrl: 'https://github.com/yourusername/canvas-game',
    liveUrl: 'https://yourcanvasgame.com',
    longDescription: 'A simple voice recognition bot made using C#...'
  },
  {
    id: 8,
    title: 'Calauan COVID-19 H.I.S',
    description: 'A web-based COVID Health information System...',
    technologies: ['PHP', 'Bootstrap 4', 'JavaScript'],
    videoId: 'QwCorZkcurk', // Replace with your YouTube video ID
    githubUrl: 'https://github.com/yourusername/weather-dashboard',
    liveUrl: 'https://yourweatherdashboard.com',
    longDescription: 'This project aims to monitor COVID-19 status at Calauan Laguna area only.'
  },

    {
    id: 9,
    title: 'BOH Consultation System',
    description: 'A web-based online consultation and appointment setter...',
    technologies: ['PHP', 'Bootstrap 4', 'JavaScript','Video Conference API'],
    videoId: 'wXaCvUfbu6Y', // Replace with your YouTube video ID
    githubUrl: 'https://github.com/yourusername/weather-dashboard',
    liveUrl: 'https://yourweatherdashboard.com',
    longDescription: 'A web-based online consultation and appointment setter...'
  },

    {
    id: 10,
    title: 'Resort Reservation System',
    description: 'A stand-alone resort reservation system made with C#...',
    technologies: ['C#.NET'],
    videoId: 'skbtqcm1x0I', // Replace with your YouTube video ID
    githubUrl: 'https://github.com/yourusername/weather-dashboard',
    liveUrl: 'https://yourweatherdashboard.com',
    longDescription: 'A stand-alone resort reservation system made with C#...'
  },

     {
    id: 11,
    title: 'Hotel Reservation System',
    description: 'A web-based hotel reservation system made with python...',
    technologies: ['Python', 'Flask','Bootstrap 4', 'JavaScript'],
    videoId: '6q6YA8Dyd7Y', // Replace with your YouTube video ID
    githubUrl: 'https://github.com/yourusername/weather-dashboard',
    liveUrl: 'https://yourweatherdashboard.com',
    longDescription: 'Accepts reservation from customers and monitor room vacancies etc..'
  },

   {
    id: 12,
    title: 'Imakorean Inventory System',
    description: 'A stand-alone inventory system made with VB.NET',
    technologies: ['VB.NET'],
    videoId: 'FH1_ba3dFmc', // Replace with your YouTube video ID
    githubUrl: 'https://github.com/yourusername/weather-dashboard',
    liveUrl: 'https://yourweatherdashboard.com',
    longDescription: 'A stand-alone inventory system made with VB.NET'
  },
   {
    id: 13,
    title: 'Dental Appointment System',
    description: 'A simple dental appointment system made with VBA..',
    technologies: ['VBA'],
    videoId: '1SY4dHuLDM0', // Replace with your YouTube video ID
    githubUrl: 'https://github.com/yourusername/weather-dashboard',
    liveUrl: 'https://yourweatherdashboard.com',
    longDescription: 'A simple dental appointment system made with VBA..'
  }

])

// Methods
const openModal = (project) => {
  selectedProject.value = project
  showModal.value = true
}

const closeModal = () => {
  showModal.value = false
  selectedProject.value = null
}

const scrollToProjects = () => {
  const element = document.getElementById('projects')
  element?.scrollIntoView({ behavior: 'smooth' })
}

// Lifecycle hooks
onMounted(() => {
  // Add scroll animations
  const observerOptions = {
    threshold: 0.1,
    rootMargin: '0px 0px -50px 0px'
  }

  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('animate-in')
      }
    })
  }, observerOptions)

  // Observe project cards after they're rendered
  setTimeout(() => {
    document.querySelectorAll('.project-card').forEach(card => {
      observer.observe(card)
    })
  }, 100)
})
</script>

<style scoped>
.portfolio-wrapper {
  min-height: 100vh;
  background-color: #0f172a;
  color: #fff;
  position: relative;
  overflow-x: hidden;
  font-family: 'Inter', sans-serif;
}

/* Animated Background */
.bg-animation {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 0;
  overflow: hidden;
  pointer-events: none;
}

.blob {
  position: absolute;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.4;
  animation: float 20s infinite;
}

.blob-1 {
  top: -10%;
  left: -10%;
  width: 50vw;
  height: 50vw;
  background: #6366f1;
  animation-delay: 0s;
}

.blob-2 {
  bottom: -10%;
  right: -10%;
  width: 50vw;
  height: 50vw;
  background: #ec4899;
  animation-delay: -5s;
}

.blob-3 {
  top: 40%;
  left: 40%;
  width: 40vw;
  height: 40vw;
  background: #8b5cf6;
  animation-delay: -10s;
}

@keyframes float {
  0%, 100% { transform: translate(0, 0) scale(1); }
  33% { transform: translate(30px, -50px) scale(1.1); }
  66% { transform: translate(-20px, 20px) scale(0.9); }
}

.hero-section {
  min-height: 100vh;
  padding: 2rem 0;
}

.glass-card {
  background: rgba(255, 255, 255, 0.03);
  backdrop-filter: blur(16px);
  -webkit-backdrop-filter: blur(16px);
  border: 1px solid rgba(255, 255, 255, 0.05);
  border-radius: 24px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
}

.bg-primary-gradient {
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
}

.gradient-text {
  background: linear-gradient(135deg, #fff 0%, #cbd5e1 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

.text-highlight {
  color: #8b5cf6;
  font-weight: 600;
}

.hover-lift {
  transition: transform 0.3s cubic-bezier(0.34, 1.56, 0.64, 1);
}

.hover-lift:hover {
  transform: translateY(-5px);
}

.btn-primary {
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  border: none;
}

.projects-section {
  padding-top: 6rem;
  padding-bottom: 6rem;
}

.divider {
  height: 4px;
  width: 60px;
  border-radius: 2px;
}

/* Custom Tabs */
.custom-nav-pills .nav-link {
  color: rgba(255, 255, 255, 0.6);
  padding: 12px 24px;
  font-weight: 500;
  transition: all 0.3s ease;
  border-radius: 50rem;
}

.custom-nav-pills .nav-link:hover {
  color: #fff;
  background: rgba(255, 255, 255, 0.05);
}

.custom-nav-pills .nav-link.active {
  background: linear-gradient(135deg, #6366f1 0%, #8b5cf6 100%);
  color: #fff;
  box-shadow: 0 4px 15px rgba(99, 102, 241, 0.35);
}

.scroll-indicator {
  position: absolute;
  bottom: 40px;
  left: 50%;
  transform: translateX(-50%);
  z-index: 10;
  text-align: center;
}

.tracking-wider {
  letter-spacing: 0.05em;
}

.tracking-widest {
  letter-spacing: 0.2em;
}

.fs-7 {
  font-size: 0.75rem;
}

/* Animations */
@keyframes fadeUpAnimation {
  from {
    opacity: 0;
    transform: translateY(40px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

@keyframes bounceAnimation {
  0%, 20%, 50%, 80%, 100% {
    transform: translateY(0) translateX(-50%);
  }
  40% {
    transform: translateY(-10px) translateX(-50%);
  }
  60% {
    transform: translateY(-5px) translateX(-50%);
  }
}

.animate-fade-up {
  animation: fadeUpAnimation 1s cubic-bezier(0.2, 0.8, 0.2, 1);
}

.animate-fade-up-delay {
  animation: fadeUpAnimation 1s cubic-bezier(0.2, 0.8, 0.2, 1) 0.2s both;
}

.animate-bounce {
  animation: bounceAnimation 2s infinite ease-in-out;
}

/* Responsive Design */
@media (max-width: 768px) {
  .display-4 {
    font-size: 2rem;
  }
  
  .display-2 {
    font-size: 2.5rem;
  }
  
  .hero-content {
    padding: 2rem !important;
  }
}

@media (max-width: 576px) {
  .custom-nav-pills {
    flex-direction: column;
    border-radius: 20px;
  }
  
  .custom-nav-pills .nav-link {
    width: 100%;
    margin-bottom: 5px;
  }
}
</style>
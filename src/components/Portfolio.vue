<template>
  <div class="portfolio-container">
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
                    class="col-lg-4 col-md-6 col-sm-12"
                  >
                    <ProjectCard 
                      :project="project" 
                      :index="index"
                      @open-modal="openModal"
                    />
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
                    class="col-lg-4 col-md-6 col-sm-12"
                  >
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
.portfolio-container {
  min-height: 100vh;
}

.hero-section {
  background: linear-gradient(135deg, rgba(102, 126, 234, 0.9) 0%, rgba(118, 75, 162, 0.9) 100%);
  position: relative;
  overflow: hidden;
}

.hero-section::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  background: url('data:image/svg+xml,<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1000 100" fill="white" opacity="0.1"><polygon points="0,0 1000,100 1000,0"/></svg>');
  background-size: cover;
}

.projects-section {
  background: rgba(255, 255, 255, 0.05);
  backdrop-filter: blur(10px);
  border-radius: 20px 20px 0 0;
  margin-top: -20px;
  position: relative;
}

.custom-tab {
  background: rgba(255, 255, 255, 0.1);
  border: 1px solid rgba(255, 255, 255, 0.2);
  color: white;
  margin: 0 5px;
  border-radius: 25px;
  padding: 12px 24px;
  transition: all 0.3s ease;
  backdrop-filter: blur(10px);
}

.custom-tab:hover {
  background: rgba(255, 255, 255, 0.2);
  transform: translateY(-2px);
  color: white;
}

.custom-tab.active {
  background: linear-gradient(45deg, #667eea, #764ba2);
  border-color: transparent;
  box-shadow: 0 8px 32px rgba(102, 126, 234, 0.3);
  color: white;
}

.scroll-indicator {
  position: absolute;
  bottom: 30px;
  left: 50%;
  transform: translateX(-50%);
  font-size: 24px;
}

/* Animations */
@keyframes fadeUpAnimation {
  from {
    opacity: 0;
    transform: translateY(30px);
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
  animation: fadeUpAnimation 1s ease-out;
}

.animate-fade-up-delay {
  animation: fadeUpAnimation 1s ease-out 0.3s both;
}

.animate-bounce {
  animation: bounceAnimation 2s infinite;
}

/* Responsive Design */
@media (max-width: 768px) {
  .hero-section {
    padding: 3rem 0;
  }
  
  .display-4 {
    font-size: 2rem;
  }
  
  .custom-tab {
    margin: 5px 0;
    padding: 10px 16px;
    font-size: 14px;
  }
}

@media (max-width: 576px) {
  .nav-pills {
    flex-direction: column;
  }
  
  .custom-tab {
    margin: 3px 0;
  }
}
</style>
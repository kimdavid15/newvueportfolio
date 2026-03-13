<template>
  <div class="portfolio">

    <!--  NAVIGATION -->
    <nav class="nav" :class="{ 'nav--scrolled': isScrolled }">
      <div class="nav__inner container">
        <a href="#hero" class="nav__logo" @click.prevent="scrollTo('#hero')">
          KDR<span class="dot">.</span>
        </a>

        <div class="nav__links" :class="{ 'nav__links--open': menuOpen }">
          <a class="nav__link" href="#about"    @click.prevent="navClick('#about')">About</a>
          <a class="nav__link" href="#skills"   @click.prevent="navClick('#skills')">Skills</a>
          <a class="nav__link" href="#projects" @click.prevent="navClick('#projects')">Projects</a>
          <a class="nav__link" href="#contact"  @click.prevent="navClick('#contact')">Contact</a>
          <a class="nav__cta btn btn--primary" href="mailto:kimdavidritardo@gmail.com">
            Hire Me
          </a>
        </div>

        <button
          class="nav__burger"
          :class="{ 'nav__burger--open': menuOpen }"
          @click="menuOpen = !menuOpen"
          aria-label="Toggle menu"
        >
          <span></span>
          <span></span>
          <span></span>
        </button>
      </div>
    </nav>

    <!-- HERO -->
    <section id="hero" class="hero">
      <div class="hero__bg-grid"></div>
      <div class="hero__glow"></div>

      <div class="hero__inner container">
        <div class="hero__content">
          <div class="hero__badge">
            <span class="hero__badge-dot"></span>
            Available for opportunities
          </div>

          <h1 class="hero__title">
            <span class="hero__title-name">Kim David</span>
            <span class="hero__title-name hero__title-name--outline">Ritardo</span>
          </h1>

          <p class="hero__role">
            Web Developer
          </p>

          <p class="hero__desc">
            I design and build high-performance web applications from intuitive frontends
            to robust backend systems â€” with a relentless focus on clean code and real-world impact.
          </p>

          <div class="hero__actions">
            <a href="#projects" class="btn btn--primary" @click.prevent="scrollTo('#projects')">
              View My Work <i class="fas fa-arrow-down"></i>
            </a>
            <a href="#contact" class="btn btn--ghost" @click.prevent="scrollTo('#contact')">
              Get In Touch
            </a>
          </div>
        </div>

        <div class="hero__scroll-hint">
          <span class="hero__scroll-label">Scroll</span>
          <div class="hero__scroll-line"></div>
        </div>
      </div>
    </section>

    <!-- ABOUT -->
    <section id="about" class="about section">
      <div class="container">
        <div class="section-label reveal">About</div>

        <div class="about__grid">
          <div class="about__left reveal">
            <div class="about__avatar">
              <div class="about__initials">KDR</div>
              <div class="about__avatar-ring"></div>
            </div>
            <div class="about__meta">
              <p class="about__name">Kim David Ritardo</p>
              <p class="about__tag">Web Developer</p>
              <p class="about__location"><i class="fas fa-map-marker-alt"></i> Philippines</p>
            </div>
          </div>

          <div class="about__right">
            <h2 class="section-title reveal">
              Turning ideas into <span class="text-gradient">digital reality.</span>
            </h2>
            <p class="about__text reveal">
              I'm a passionate web developer who thrives at the intersection of design and engineering.
              With hands-on experience across multiple stacks  PHP, Laravel, Vue.js, Python, and more. I build
              products that are fast, accessible, and a pleasure to use.
            </p>
            <p class="about__text reveal">
              Whether it's a complex inventory system, a healthcare application, or a real-time communication platform,
              I bring ideas from initial concept all the way to production deployment.
            </p>

            <div class="about__stats reveal">
              <div class="stat-card">
                <span class="stat-card__number">10+</span>
                <span class="stat-card__label">Projects created</span>
              </div>
              <div class="stat-card">
                <span class="stat-card__number">6+</span>
                <span class="stat-card__label">Technologies</span>
              </div>
              <div class="stat-card">
                <span class="stat-card__number">100%</span>
                <span class="stat-card__label">Dedication</span>
              </div>
            </div>

            <div class="about__links reveal">
              <a href="mailto:kdtechnologist@gmail.com" class="about__link">
                <i class="fas fa-envelope"></i> kdtechnologist@gmail.com
              </a>
              <a href="https://github.com/kimdavid15" target="_blank" rel="noopener noreferrer" class="about__link">
                <i class="fab fa-github"></i> GitHub
              </a>
              <a href="www.linkedin.com/in/kd1501" target="_blank" rel="noopener noreferrer" class="about__link">
                <i class="fab fa-linkedin"></i> LinkedIn
              </a>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!--  SKILLS -->
    <section id="skills" class="skills section section--alt">
      <div class="container">
        <div class="section-label reveal">Skills</div>
        <h2 class="section-title reveal">Tech Stack &amp; <span class="text-gradient">Expertise</span></h2>
        <p class="section-desc reveal">A curated set of tools, languages, and frameworks I work with to build complete solutions.</p>

        <div class="skills__grid">
          <div
            v-for="(cat, i) in skillCategories"
            :key="cat.name"
            class="skill-card reveal"
            :style="{ transitionDelay: `${i * 80}ms` }"
          >
            <div class="skill-card__header">
              <div class="skill-card__icon">
                <i :class="cat.icon"></i>
              </div>
              <h3 class="skill-card__title">{{ cat.name }}</h3>
            </div>
            <div class="skill-tags">
              <span v-for="s in cat.skills" :key="s" class="skill-tag">{{ s }}</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!--  PROJECTS -->
    <section id="projects" class="projects section">
      <div class="container">
        <div class="section-label reveal">Work</div>
        <h2 class="section-title reveal">Featured <span class="text-gradient">Projects</span></h2>
        <p class="section-desc reveal">A showcase of real-world applications I've designed, built, and shipped.</p>

        <div class="tab-bar reveal">
          <button
            class="tab-btn"
            :class="{ 'tab-btn--active': activeTab === 'latest' }"
            @click="activeTab = 'latest'"
          >
            <i class="fas fa-layer-group"></i> Modern Stack
          </button>
          <button
            class="tab-btn"
            :class="{ 'tab-btn--active': activeTab === 'vanilla' }"
            @click="activeTab = 'vanilla'"
          >
            <i class="fas fa-code"></i> Classic Projects
          </button>
          <div class="tab-bar__indicator" :style="tabIndicatorStyle"></div>
        </div>

        <div class="project-grid">
          <ProjectCard
            v-for="(project, index) in activeProjects"
            :key="project.id"
            :project="project"
            :index="index"
            @open-modal="openModal"
          />
        </div>
      </div>
    </section>

    <!-- CONTACT -->
    <section id="contact" class="contact section section--alt">
      <div class="container">
        <div class="section-label reveal">Contact</div>
        <div class="contact__inner">
          <h2 class="contact__heading reveal">
            Let's build something <span class="text-gradient">great together.</span>
          </h2>
          <p class="contact__desc reveal">
            I'm currently open to new opportunities freelance, full-time, or collaboration.
            If you have a project in mind or just want to connect, I'd love to hear from you.
          </p>
          <a href="mailto:kdtechnologist@gmail.com" class="btn btn--primary btn--lg reveal">
            Say Hello <i class="fas fa-paper-plane"></i>
          </a>

          <div class="social-row reveal">
            <a href="https://github.com/kimdavid15" target="_blank" rel="noopener noreferrer" class="social-btn" aria-label="GitHub">
              <i class="fab fa-github"></i>
            </a>
            <a href="https://www.linkedin.com/in/kd1501/" target="_blank" rel="noopener noreferrer" class="social-btn" aria-label="LinkedIn">
              <i class="fab fa-linkedin-in"></i>
            </a>
            <a href="https://web.facebook.com/kr0015" target="_blank" rel="noopener noreferrer" class="social-btn" aria-label="Facebook">
              <i class="fab fa-facebook-f"></i>
            </a>
            <a href="mailto:kdtechnologist@gmail.com" class="social-btn" aria-label="Email">
              <i class="fas fa-envelope"></i>
            </a>
          </div>
        </div>
      </div>
    </section>

    <!-- FOOTER -->
    <footer class="footer">
      <div class="container">
        <div class="footer__inner">
          <span class="footer__logo">KDR<span class="dot">.</span></span>
          <p class="footer__copy">
            Designed &amp; built by <strong>Kim David Ritardo</strong> &copy; {{ currentYear }}
          </p>
          <p class="footer__stack">Built with Vue.js &amp; Vite</p>
        </div>
      </div>
    </footer>

    <!-- MODAL -->
    <ProjectModal
      :project="selectedProject"
      :show="showModal"
      @close="closeModal"
    />

  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import ProjectCard from './ProjectCard.vue'
import ProjectModal from './ProjectModal.vue'


const activeTab       = ref('latest')
const showModal       = ref(false)
const selectedProject = ref(null)
const isScrolled      = ref(false)
const menuOpen        = ref(false)
const currentYear     = new Date().getFullYear()


const skillCategories = [
  {
    name: 'Frontend',
    icon: 'fas fa-palette',
    skills: ['HTML5', 'CSS3', 'JavaScript', 'Vue.js', 'Bootstrap', 'jQuery']
  },
  {
    name: 'Backend',
    icon: 'fas fa-server',
    skills: ['PHP', 'Laravel', 'Python', 'Flask', 'C#.NET', 'VB.NET', 'CodeIgniter']
  },
  {
    name: 'Database',
    icon: 'fas fa-database',
    skills: ['MySQL', 'SQLite', 'SQL Server', 'MS Access']
  },
  {
    name: 'Tools & Others',
    icon: 'fas fa-tools',
    skills: ['Git', 'VS Code', 'Postman', 'REST APIs', 'SMS API', 'Voice Recognition']
  }
]


const latestProjects = ref([
  {
    id: 1,
    title: 'LU Chats',
    description: 'A fully responsive messaging web app providing seamless communication between students and faculty at Laguna University.',
    technologies: ['PHP', 'Laravel', 'Bootstrap', 'JavaScript'],
    videoId: 'CRYmVVQ9R5Q',
    longDescription: 'This project is a fully responsive web application designed to provide simple, real-time-like communication between students and faculty at Laguna University. It features user authentication, conversation threading, and a clean mobile-first UI.'
  },
  {
    id: 2,
    title: 'LU Supply Office System',
    description: 'A full-featured web inventory management system for the Supply Office of Laguna University.',
    technologies: ['PHP', 'Laravel 10', 'Bootstrap', 'JavaScript'],
    videoId: 'kMFIr-V82aY',
    longDescription: 'A comprehensive web inventory system built with PHP Laravel 10. Manages supply requests, stock tracking, and reporting for the university supply office with role-based access control.'
  }
])

const vanillaProjects = ref([
  {
    id: 5,
    title: 'e-Commerce Project',
    description: 'A fully functional e-commerce platform developed during an internship at Village88 Inc.',
    technologies: ['PHP', 'CodeIgniter', 'Bootstrap', 'JavaScript'],
    videoId: 'h2QoEEtr_Qw',
    longDescription: 'Created during my internship at Village88 Inc. A complete e-commerce site with product browsing, cart functionality, and order processing built on CodeIgniter.'
  },
  {
    id: 6,
    title: 'Crime Monitoring & Analysis',
    description: 'A web-based crime monitoring, reporting, and statistical analysis platform with SMS notifications.',
    technologies: ['PHP', 'Bootstrap', 'JavaScript', 'SMS API'],
    videoId: 'IuDbhb7Q0Pk',
    longDescription: 'A web-based crime monitoring, reporting, and analysis system that integrates SMS API for real-time notifications to authorities and community members.'
  },
  {
    id: 7,
    title: 'Pharmabot',
    description: 'An intelligent voice recognition pharmaceutical assistant built with C# and external microphone input.',
    technologies: ['C#.NET', 'Voice Recognition', 'External Microphone'],
    videoId: 'MbE1aleSOZU',
    longDescription: 'A desktop voice recognition bot built using C# that assists with pharmaceutical queries. Uses an external microphone and speech recognition libraries for natural language interaction.'
  },
  {
    id: 8,
    title: 'Calauan COVID-19 H.I.S',
    description: 'A web-based COVID-19 Health Information System for monitoring and managing cases in Calauan, Laguna.',
    technologies: ['PHP', 'Bootstrap', 'JavaScript'],
    videoId: 'QwCorZkcurk',
    longDescription: 'This project aims to monitor COVID-19 status and case management for the Calauan, Laguna area. Features real-time case tracking, reporting dashboards, and health status monitoring.'
  },
  {
    id: 9,
    title: 'BOH Consultation System',
    description: 'A web-based online consultation and appointment management system with integrated video conferencing.',
    technologies: ['PHP', 'Bootstrap', 'JavaScript', 'Video Conference API'],
    videoId: 'wXaCvUfbu6Y',
    longDescription: 'A web-based online consultation and appointment setter with integrated video conferencing capabilities for a Bureau of Health facility.'
  },
  {
    id: 10,
    title: 'Resort Reservation System',
    description: 'A desktop resort reservation and management system with booking, availability tracking, and reporting.',
    technologies: ['C#.NET'],
    videoId: 'skbtqcm1x0I',
    longDescription: 'A stand-alone desktop resort reservation system built with C#.NET. Manages room bookings, guest records, availability calendars, and printable reports.'
  },
  {
    id: 11,
    title: 'Hotel Reservation System',
    description: 'A web-based hotel reservation system with customer booking, room management, and vacancy monitoring.',
    technologies: ['Python', 'Flask', 'Bootstrap', 'JavaScript'],
    videoId: '6q6YA8Dyd7Y',
    longDescription: 'Built with Python Flask, this system accepts online reservations from customers, manages room vacancies, and provides an admin dashboard for hotel operations.'
  },
  {
    id: 12,
    title: 'Imakorean Inventory System',
    description: 'A stand-alone desktop inventory management system for a Korean restaurant business.',
    technologies: ['VB.NET'],
    videoId: 'FH1_ba3dFmc',
    longDescription: 'A stand-alone inventory system made with VB.NET, designed specifically for Imakorean restaurant to manage stock, suppliers, and inventory reports.'
  },
  {
    id: 13,
    title: 'Dental Appointment System',
    description: 'A desktop dental clinic appointment scheduler and patient record management system.',
    technologies: ['VBA'],
    videoId: '1SY4dHuLDM0',
    longDescription: 'A simple but complete dental appointment system built with VBA. Manages patient records, appointment scheduling, and basic billing within a Microsoft Office environment.'
  }
])


const activeProjects = computed(() =>
  activeTab.value === 'latest' ? latestProjects.value : vanillaProjects.value
)

const tabIndicatorStyle = computed(() => ({
  transform: activeTab.value === 'latest' ? 'translateX(0%)' : 'translateX(100%)',
  width: '50%'
}))

const openModal = (project) => {
  selectedProject.value = project
  showModal.value = true
}

const closeModal = () => {
  showModal.value = false
  selectedProject.value = null
}

const scrollTo = (selector) => {
  menuOpen.value = false
  document.querySelector(selector)?.scrollIntoView({ behavior: 'smooth' })
}

const navClick = (selector) => {
  menuOpen.value = false
  setTimeout(() => {
    document.querySelector(selector)?.scrollIntoView({ behavior: 'smooth' })
  }, 50)
}

const handleScroll = () => {
  isScrolled.value = window.scrollY > 60
}

const setupReveal = () => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('revealed')
          observer.unobserve(entry.target)
        }
      })
    },
    { threshold: 0.1, rootMargin: '0px 0px -60px 0px' }
  )
  document.querySelectorAll('.reveal').forEach((el) => observer.observe(el))
}


onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
  setTimeout(setupReveal, 120)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<style scoped>

.nav {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 1000;
  padding: 20px 0;
  transition: padding 0.3s ease, background 0.3s ease, border-bottom 0.3s ease;
  border-bottom: 1px solid transparent;
}
.nav--scrolled {
  padding: 14px 0;
  background: rgba(8, 8, 8, 0.85);
  backdrop-filter: blur(20px);
  -webkit-backdrop-filter: blur(20px);
  border-bottom-color: var(--border);
}
.nav__inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.nav__logo {
  font-size: 1.15rem;
  font-weight: 800;
  letter-spacing: -0.02em;
  color: var(--text-1);
  transition: color 0.2s;
}
.nav__logo:hover { color: var(--white); }
.dot { color: var(--text-3); }

.nav__links {
  display: flex;
  align-items: center;
  gap: 32px;
}
.nav__link {
  font-size: 0.88rem;
  font-weight: 500;
  color: var(--text-2);
  transition: color 0.2s;
  letter-spacing: 0.01em;
}
.nav__link:hover { color: var(--white); }
.nav__cta {
  padding: 9px 20px;
  font-size: 0.85rem;
}

.nav__burger {
  display: none;
  flex-direction: column;
  gap: 5px;
  padding: 4px;
}
.nav__burger span {
  display: block;
  width: 22px;
  height: 2px;
  background: var(--text-2);
  border-radius: 2px;
  transition: all 0.3s ease;
  transform-origin: center;
}
.nav__burger--open span:nth-child(1) { transform: translateY(7px) rotate(45deg); }
.nav__burger--open span:nth-child(2) { opacity: 0; transform: scaleX(0); }
.nav__burger--open span:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }


.hero {
  position: relative;
  min-height: 100vh;
  display: flex;
  align-items: center;
  overflow: hidden;
  background: var(--bg-0);
}

/* Grid background */
.hero__bg-grid {
  position: absolute;
  inset: 0;
  background-image:
    linear-gradient(rgba(255,255,255,0.026) 1px, transparent 1px),
    linear-gradient(90deg, rgba(255,255,255,0.026) 1px, transparent 1px);
  background-size: 64px 64px;
  -webkit-mask-image: radial-gradient(ellipse 80% 70% at 50% 40%, black 30%, transparent 80%);
  mask-image: radial-gradient(ellipse 80% 70% at 50% 40%, black 30%, transparent 80%);
  pointer-events: none;
}

/* Subtle white glow top-right */
.hero__glow {
  position: absolute;
  top: -200px;
  right: -200px;
  width: 700px;
  height: 700px;
  background: radial-gradient(circle, rgba(255,255,255,0.028) 0%, transparent 65%);
  pointer-events: none;
}

.hero__inner {
  position: relative;
  width: 100%;
  padding-top: 100px;
  padding-bottom: 80px;
}
.hero__content { max-width: 780px; }

/* Badge */
.hero__badge {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 7px 14px;
  border-radius: 100px;
  border: 1px solid var(--border-md);
  background: rgba(255,255,255,0.04);
  font-family: var(--font-mono);
  font-size: 0.72rem;
  font-weight: 500;
  letter-spacing: 0.08em;
  color: var(--text-2);
  text-transform: uppercase;
  margin-bottom: 32px;
}
.hero__badge-dot {
  width: 7px;
  height: 7px;
  border-radius: 50%;
  background: #4ade80;
  box-shadow: 0 0 8px rgba(74,222,128,0.7);
  animation: pulse-dot 2.4s infinite;
}
@keyframes pulse-dot {
  0%, 100% { opacity: 1; transform: scale(1); }
  50%       { opacity: 0.6; transform: scale(0.8); }
}

/* Giant title */
.hero__title {
  font-size: clamp(4.2rem, 11vw, 10rem);
  font-weight: 900;
  line-height: 0.92;
  letter-spacing: -0.04em;
  margin-bottom: 32px;
}
.hero__title-name {
  display: block;
  color: var(--white);
}
.hero__title-name--outline {
  color: transparent;
  -webkit-text-stroke: 1.5px rgba(255,255,255,0.45);
}

.hero__role {
  font-family: var(--font-mono);
  font-size: clamp(0.9rem, 2vw, 1.1rem);
  font-weight: 400;
  color: var(--text-2);
  letter-spacing: 0.04em;
  margin-bottom: 20px;
}

.hero__desc {
  font-size: clamp(1rem, 1.8vw, 1.15rem);
  color: var(--text-2);
  max-width: 560px;
  line-height: 1.7;
  margin-bottom: 40px;
}

.hero__actions {
  display: flex;
  gap: 14px;
  flex-wrap: wrap;
}

/* Scroll hint */
.hero__scroll-hint {
  position: absolute;
  bottom: 36px;
  left: 24px;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 8px;
}
.hero__scroll-label {
  font-family: var(--font-mono);
  font-size: 0.65rem;
  font-weight: 500;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--text-3);
  writing-mode: vertical-rl;
}
.hero__scroll-line {
  width: 1px;
  height: 56px;
  background: linear-gradient(to bottom, var(--text-3), transparent);
  margin-left: 3px;
  animation: scroll-hint 2s ease-in-out infinite;
}
@keyframes scroll-hint {
  0%, 100% { opacity: 0.4; transform: scaleY(1); }
  50%       { opacity: 1;   transform: scaleY(0.6) translateY(30%); }
}


.about__grid {
  display: grid;
  grid-template-columns: 240px 1fr;
  gap: 80px;
  align-items: start;
}

.about__left {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
  position: sticky;
  top: 100px;
}

.about__avatar {
  position: relative;
  width: 140px;
  height: 140px;
}

.about__initials {
  width: 140px;
  height: 140px;
  border-radius: 50%;
  background: var(--bg-3);
  border: 1px solid var(--border-md);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1.8rem;
  font-weight: 800;
  letter-spacing: -0.02em;
  color: var(--text-2);
}

.about__avatar-ring {
  position: absolute;
  inset: -6px;
  border-radius: 50%;
  border: 1px solid var(--border);
}

.about__meta { text-align: center; }
.about__name {
  font-size: 0.95rem;
  font-weight: 700;
  color: var(--text-1);
  margin-bottom: 4px;
}
.about__tag {
  font-family: var(--font-mono);
  font-size: 0.72rem;
  color: var(--text-3);
  letter-spacing: 0.06em;
  margin-bottom: 8px;
}
.about__location {
  font-size: 0.8rem;
  color: var(--text-3);
}
.about__location i { margin-right: 5px; }

.about__text {
  font-size: 1.05rem;
  color: var(--text-2);
  line-height: 1.75;
  margin-bottom: 18px;
}

.about__stats {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  margin: 32px 0;
}
.stat-card {
  padding: 20px 16px;
  background: var(--bg-2);
  border: 1px solid var(--border);
  border-radius: 10px;
  text-align: center;
  transition: border-color 0.25s;
}
.stat-card:hover { border-color: var(--border-high); }
.stat-card__number {
  display: block;
  font-size: 1.9rem;
  font-weight: 800;
  letter-spacing: -0.04em;
  color: var(--white);
  margin-bottom: 4px;
}
.stat-card__label {
  font-size: 0.75rem;
  color: var(--text-3);
  letter-spacing: 0.04em;
  font-weight: 500;
}

.about__links {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
}
.about__link {
  display: inline-flex;
  align-items: center;
  gap: 7px;
  padding: 9px 16px;
  border-radius: 6px;
  border: 1px solid var(--border);
  font-size: 0.82rem;
  font-weight: 500;
  color: var(--text-2);
  transition: all 0.2s;
  background: var(--bg-2);
}
.about__link:hover {
  border-color: var(--border-high);
  color: var(--white);
  background: var(--bg-3);
}


.skills__grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  gap: 20px;
}

.skill-card {
  padding: 28px;
  background: var(--bg-2);
  border: 1px solid var(--border);
  border-radius: 14px;
  transition: all 0.25s var(--ease);
}
.skill-card:hover {
  border-color: var(--border-md);
  background: var(--bg-3);
  transform: translateY(-3px);
}

.skill-card__header {
  display: flex;
  align-items: center;
  gap: 12px;
  margin-bottom: 20px;
}
.skill-card__icon {
  width: 38px;
  height: 38px;
  border-radius: 8px;
  background: var(--bg-3);
  border: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 0.9rem;
  color: var(--text-2);
}
.skill-card__title {
  font-size: 0.92rem;
  font-weight: 700;
  color: var(--text-1);
  letter-spacing: -0.01em;
}

.skill-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 7px;
}
.skill-tag {
  padding: 5px 11px;
  border-radius: 100px;
  border: 1px solid var(--border);
  font-size: 0.76rem;
  font-weight: 500;
  color: var(--text-2);
  background: var(--bg-0);
  transition: all 0.2s;
}
.skill-tag:hover {
  border-color: var(--border-high);
  color: var(--white);
}


.tab-bar {
  position: relative;
  display: inline-flex;
  background: var(--bg-2);
  border: 1px solid var(--border);
  border-radius: 8px;
  padding: 4px;
  margin-bottom: 40px;
  gap: 0;
}

.tab-btn {
  position: relative;
  z-index: 1;
  padding: 9px 22px;
  border-radius: 5px;
  font-size: 0.85rem;
  font-weight: 600;
  color: var(--text-3);
  transition: color 0.25s;
  display: flex;
  align-items: center;
  gap: 7px;
  white-space: nowrap;
}
.tab-btn--active { color: var(--white); }
.tab-btn:hover:not(.tab-btn--active) { color: var(--text-2); }

.tab-bar__indicator {
  position: absolute;
  top: 4px;
  left: 4px;
  height: calc(100% - 8px);
  background: var(--bg-4);
  border: 1px solid var(--border-md);
  border-radius: 5px;
  transition: transform 0.3s var(--ease);
  pointer-events: none;
}

.project-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 22px;
}


.contact__inner {
  max-width: 640px;
}
.contact__heading {
  font-size: clamp(2rem, 4vw, 2.8rem);
  font-weight: 800;
  letter-spacing: -0.03em;
  line-height: 1.2;
  margin-bottom: 18px;
}
.contact__desc {
  font-size: 1.05rem;
  color: var(--text-2);
  margin-bottom: 36px;
  line-height: 1.7;
}

.social-row {
  display: flex;
  gap: 12px;
  margin-top: 32px;
}
.social-btn {
  width: 46px;
  height: 46px;
  border-radius: 8px;
  background: var(--bg-2);
  border: 1px solid var(--border);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--text-2);
  font-size: 0.95rem;
  transition: all 0.2s;
}
.social-btn:hover {
  border-color: var(--border-high);
  color: var(--white);
  background: var(--bg-3);
  transform: translateY(-2px);
}

.footer {
  padding: 40px 0;
  border-top: 1px solid var(--border);
  background: var(--bg-0);
}
.footer__inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  flex-wrap: wrap;
  gap: 12px;
}
.footer__logo {
  font-size: 1rem;
  font-weight: 800;
  letter-spacing: -0.02em;
  color: var(--text-2);
}
.footer__copy {
  font-size: 0.82rem;
  color: var(--text-3);
}
.footer__copy strong { color: var(--text-2); font-weight: 600; }
.footer__stack {
  font-family: var(--font-mono);
  font-size: 0.72rem;
  color: var(--text-3);
  letter-spacing: 0.06em;
}

@media (max-width: 1024px) {
  .about__grid {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  .about__left {
    flex-direction: row;
    align-items: center;
    position: static;
    gap: 24px;
  }
  .about__meta { text-align: left; }
}

@media (max-width: 768px) {
  .nav__links {
    position: fixed;
    top: 0;
    right: 0;
    bottom: 0;
    width: 280px;
    flex-direction: column;
    align-items: flex-start;
    justify-content: center;
    padding: 40px 32px;
    gap: 24px;
    background: var(--bg-1);
    border-left: 1px solid var(--border);
    transform: translateX(100%);
    transition: transform 0.35s var(--ease);
    z-index: 999;
  }
  .nav__links--open { transform: translateX(0); }
  .nav__link { font-size: 1.1rem; }
  .nav__cta { align-self: flex-start; }
  .nav__burger { display: flex; }

  .hero__title { margin-bottom: 24px; }
  .hero__actions { flex-direction: column; }
  .hero__actions .btn { width: 100%; justify-content: center; }

  .about__stats { grid-template-columns: repeat(3, 1fr); }

  .project-grid {
    grid-template-columns: repeat(auto-fill, minmax(260px, 1fr));
  }
}

@media (max-width: 480px) {
  .about__stats { grid-template-columns: repeat(3, 1fr); gap: 10px; }
  .stat-card__number { font-size: 1.5rem; }
  .tab-bar { width: 100%; }
  .tab-btn { flex: 1; justify-content: center; }
  .tab-bar__indicator { width: 50%; }
  .footer__inner { flex-direction: column; align-items: flex-start; }
}
</style>

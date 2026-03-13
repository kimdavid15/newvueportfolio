<template>
  <Portfolio />
</template>

<script setup>
import Portfolio from './components/Portfolio.vue'
</script>

<style>
/* ─── CSS Custom Properties ─────────────────────── */
:root {
  --bg-0:        #080808;
  --bg-1:        #0f0f0f;
  --bg-2:        #161616;
  --bg-3:        #1f1f1f;
  --bg-4:        #2a2a2a;
  --border:      rgba(255, 255, 255, 0.07);
  --border-md:   rgba(255, 255, 255, 0.13);
  --border-high: rgba(255, 255, 255, 0.22);
  --text-1:      #f0f0f0;
  --text-2:      #a0a0a0;
  --text-3:      #606060;
  --white:       #ffffff;
  --font-sans:   'Inter', -apple-system, BlinkMacSystemFont, sans-serif;
  --font-mono:   'JetBrains Mono', 'Fira Code', monospace;
  --ease:        cubic-bezier(0.4, 0, 0.2, 1);
  --ease-spring: cubic-bezier(0.34, 1.56, 0.64, 1);
}

/* ─── Reset ─────────────────────────────────────── */
*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
  font-size: 16px;
}

body {
  font-family: var(--font-sans);
  background-color: var(--bg-0);
  color: var(--text-1);
  line-height: 1.6;
  overflow-x: hidden;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

img   { max-width: 100%; display: block; }
a     { text-decoration: none; color: inherit; }
button { cursor: pointer; border: none; background: none; font-family: inherit; }
ul    { list-style: none; }

/* ─── Scrollbar ──────────────────────────────────── */
::-webkit-scrollbar              { width: 5px; }
::-webkit-scrollbar-track        { background: var(--bg-0); }
::-webkit-scrollbar-thumb        { background: var(--bg-4); border-radius: 3px; }
::-webkit-scrollbar-thumb:hover  { background: var(--text-3); }

/* ─── Text selection ─────────────────────────────── */
::selection {
  background: rgba(255, 255, 255, 0.12);
  color: var(--white);
}

/* ─── Reveal animation base ──────────────────────── */
.reveal {
  opacity: 0;
  transform: translateY(28px);
  transition: opacity 0.75s var(--ease), transform 0.75s var(--ease);
}
.reveal.revealed {
  opacity: 1;
  transform: translateY(0);
}

/* ─── Global container ───────────────────────────── */
.container {
  width: 100%;
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 24px;
}

/* ─── Global button styles ───────────────────────── */
.btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 12px 28px;
  border-radius: 6px;
  font-size: 0.9rem;
  font-weight: 600;
  letter-spacing: 0.02em;
  transition: all 0.25s var(--ease);
  cursor: pointer;
}
.btn--primary {
  background: var(--white);
  color: #080808;
  border: 1px solid var(--white);
}
.btn--primary:hover {
  background: transparent;
  color: var(--white);
}
.btn--ghost {
  background: transparent;
  color: var(--text-1);
  border: 1px solid var(--border-md);
}
.btn--ghost:hover {
  border-color: var(--border-high);
  color: var(--white);
  background: rgba(255,255,255,0.04);
}
.btn--lg {
  padding: 15px 38px;
  font-size: 1rem;
}

/* ─── Section utilities ──────────────────────────── */
.section { padding: 120px 0; }
.section--alt { background: var(--bg-1); }

.section-label {
  font-family: var(--font-mono);
  font-size: 0.72rem;
  font-weight: 500;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--text-3);
  margin-bottom: 16px;
}

.section-title {
  font-size: clamp(2rem, 4vw, 3rem);
  font-weight: 800;
  line-height: 1.15;
  letter-spacing: -0.03em;
  color: var(--text-1);
  margin-bottom: 16px;
}

.section-desc {
  font-size: 1.05rem;
  color: var(--text-2);
  max-width: 560px;
  margin-bottom: 56px;
}

.text-gradient {
  background: linear-gradient(135deg, var(--white) 0%, #888888 100%);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
}

@media (max-width: 768px) {
  .section { padding: 80px 0; }
  .container { padding: 0 20px; }
}
</style>

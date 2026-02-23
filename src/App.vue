<script setup>
import { RouterLink, RouterView } from 'vue-router'
import DmLogo from './components/DmLogo.vue'
</script>

<template>
  <div class="app-wrapper">

    <header class="top-nav no-print">
      <div class="brand">
        <RouterLink to="/" class="logo-link">
          <DmLogo size="2.2rem" />
        </RouterLink>
      </div>

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/about">About</RouterLink>
        <RouterLink to="/resume">Resume</RouterLink>
        <RouterLink to="/projects">Projects</RouterLink>
      </nav>
    </header>

    <main class="content">
      <RouterView />
    </main>

    <div class="footer-connect no-print">
      <a href="https://www.linkedin.com/in/dmorton714/" target="_blank" rel="noopener noreferrer">
        <img src="/ln.png" alt="LinkedIn" class="social-icon" />
      </a>

      <a href="https://github.com/dmorton714" target="_blank" rel="noopener noreferrer">
        <img src="/git.svg" alt="GitHub" class="social-icon" />
      </a>

      <a href="mailto:danny.morton714@gmail.com" target="_blank" rel="noopener noreferrer">
        <img src="/email.png" alt="Email" class="social-icon" />
      </a>

      <a href="https://www.kycolonels.org/" target="_blank" rel="noopener noreferrer">
        <img src="/colonel.png" alt="Colonels Logo" class="social-icon" />
      </a>
    </div>

  </div>
</template>

<style scoped>
.app-wrapper {
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  width: 100%;
  background-color: #f8fafc;
  padding-bottom: 70px;
}

.top-nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 1.2rem 2rem;
  background-color: white;
  border-bottom: 1px solid #e2e8f0;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.05);
}

.logo-link {
  text-decoration: none;
  display: flex;
  align-items: center;
}

nav {
  display: flex;
  gap: 1.1rem;
  align-items: center;
}

nav a {
  text-decoration: none;
  color: #64748b;
  font-weight: 500;
  font-size: 1rem;
  transition: color 0.2s ease;
}

nav a:hover {
  color: #2563eb;
}

nav a.router-link-exact-active {
  color: #0f172a;
  font-weight: 600;
}

.content {
  flex: 1;
  width: 100%;
  max-width: 100%;
  /* margin: 0 auto; */
}

.footer-connect {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  display: flex;
  justify-content: center;
  gap: 20px;
  padding: 15px;
  background: white;
  border-top: 1px solid #e2e8f0;
  box-shadow: 0 -4px 6px -1px rgba(0, 0, 0, 0.05);
  z-index: 1000;
}

.social-icon {
  width: 28px;
  height: 28px;
  object-fit: contain;
  opacity: 0.6;
  transition: all 0.2s ease;
}

.social-icon:hover {
  opacity: 1;
  transform: translateY(-3px);
}

@media print {
  .no-print, .footer-connect {
    display: none !important;
  }
  .content {
    padding: 0;
    margin: 0;
    max-width: 100%;
  }
  .app-wrapper {
    background-color: white;
  }
}
</style>

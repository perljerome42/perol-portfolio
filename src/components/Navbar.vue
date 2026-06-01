<script setup>
import siteData from '../data/siteData.json'
</script>

<template>
  <nav id="navbar" class="navbar fixed-top navbar-expand-lg py-0">
    <div class="container d-flex align-items-center justify-content-between h-100">
      <a class="nav-brand text-decoration-none" href="#landing">{{ siteData.navbar.brand }}</a>
      <button class="navbar-toggler border-0" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse justify-content-end" id="navbarNav">
        <ul class="navbar-nav">
          <li v-for="link in siteData.navbar.links" :key="link.text" class="nav-item">
            <a class="nav-link" :class="{ active: link.active }" :href="link.href">{{ link.text }}</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<style scoped>
#navbar {
  top: 0; left: 0; right: 0;
  height: var(--nav-height);
  z-index: 1000;
  background: rgba(8, 12, 16, 0.85) !important;
  backdrop-filter: blur(16px);
  border-bottom: 1px solid var(--border);
}

.nav-brand {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  font-size: 1.2rem;
  color: var(--accent) !important;
  letter-spacing: 0.05em;
}

.navbar-nav { gap: 0.25rem; }

#navbar .nav-link {
  font-family: 'DM Mono', monospace;
  font-size: 0.78rem;
  color: var(--text-secondary) !important;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  padding: 0.45rem 1rem !important;
  border-radius: 6px;
  transition: color 0.2s, background 0.2s;
}

#navbar .nav-link:hover,
#navbar .nav-link.active {
  color: var(--accent) !important;
  background: var(--accent-dim);
}

.navbar-toggler { border-color: var(--border) !important; }

.navbar-toggler-icon {
  background-image: url("data:image/svg+xml,%3csvg xmlns='http://www.w3.org/2000/svg' viewBox='0 0 30 30'%3e%3cpath stroke='rgba%2874,244,194,0.8%29' stroke-linecap='round' stroke-miterlimit='10' stroke-width='2' d='M4 7h22M4 15h22M4 23h22'/%3e%3c/svg%3e") !important;
}

.navbar { padding: 0 !important; }
.navbar-collapse {
  background: rgba(8, 12, 16, 0.98);
  border-radius: 10px;
  margin-top: 0.5rem;
  padding: 0.75rem;
}
@media (min-width: 992px) {
  .navbar-collapse { background: transparent; margin-top: 0; padding: 0; }
}
</style>

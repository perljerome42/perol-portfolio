<script setup>
import projects from '../data/projects.json'
import siteData from '../data/siteData.json'
</script>

<template>
  <section id="projects" class="position-relative">
    <div class="container">
      <div class="text-center reveal">
        <p class="section-label">{{ siteData.projects.label }}</p>
        <h2 class="section-title">{{ siteData.projects.title }}</h2>
      </div>
      <div class="project-grid d-grid">
        <div class="project-card reveal" v-for="project in projects" :key="project.id">
          <div class="card-img-wrap">
            <img :src="project.image" :alt="project.title">
            <div class="card-img-overlay-accent"></div>
          </div>
          <div class="card-body">
            <span class="card-tag">{{ project.tag }}</span>
            <h5 class="card-title-custom">{{ project.title }}</h5>
            <p class="card-desc">{{ project.description }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
#projects {
  padding: 7rem 0;
  z-index: 1;
}

.project-grid {
  grid-template-columns: repeat(auto-fill, minmax(320px, 1fr));
  gap: 1.5rem;
  margin-top: 3.5rem;
}

.project-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 16px;
  overflow: hidden;
  transition: transform 0.3s, border-color 0.3s, box-shadow 0.3s;
  cursor: pointer;
  position: relative;
}

.project-card:hover {
  transform: translateY(-6px);
  border-color: var(--border-hover);
  box-shadow: 0 20px 60px rgba(0,0,0,0.4), 0 0 30px var(--accent-dim);
}

.card-img-wrap {
  overflow: hidden;
  height: 200px;
  background: var(--bg-secondary);
  position: relative;
}

.card-img-wrap img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.4s, filter 0.4s;
  filter: grayscale(30%) brightness(0.8);
}

.project-card:hover .card-img-wrap img {
  transform: scale(1.05);
  filter: grayscale(0%) brightness(1);
}

.card-img-overlay-accent {
  position: absolute;
  inset: 0;
  background: linear-gradient(to top, var(--bg-card) 0%, transparent 50%);
}

.card-body { padding: 1.4rem; }

.card-tag {
  font-family: 'DM Mono', monospace;
  font-size: 0.65rem;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: var(--accent);
  background: var(--accent-dim);
  border-radius: 4px;
  padding: 0.2rem 0.55rem;
  display: inline-block;
  margin-bottom: 0.75rem;
}

.card-title-custom {
  font-family: 'Syne', sans-serif;
  font-size: 1rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 0.65rem;
  line-height: 1.3;
}

.card-desc {
  font-size: 0.84rem;
  color: var(--text-secondary);
  line-height: 1.65;
}
</style>

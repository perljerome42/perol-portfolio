<script setup>
import tools from '../data/tools.json'
import siteData from '../data/siteData.json'
</script>

<template>
  <section id="tools" class="position-relative">
    <div class="container">
      <div class="text-center reveal">
        <p class="section-label">{{ siteData.tools.label }}</p>
        <h2 class="section-title">{{ siteData.tools.title }}</h2>
      </div>
      <div class="tools-grid d-grid">
        <div class="tools-category reveal text-center" v-for="category in tools" :key="category.id">
          <p class="tools-cat-label">{{ category.label }}</p>
          <h3 class="tools-cat-title text-center">{{ category.title }}</h3>
          <div class="tool-logos d-flex flex-wrap justify-content-center mt-4">
            <div class="tool-item d-flex flex-column align-items-center col-4 col-md-4" v-for="tool in category.tools" :key="tool.name">
              <img :src="tool.image" :alt="tool.name">
              <span>{{ tool.name }}</span>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
#tools {
  padding: 7rem 0;
  z-index: 1;
}

.tools-grid {
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
  margin-top: 3.5rem;
}

@media (max-width: 768px) {
  .tools-grid { grid-template-columns: 1fr; }
}

.tools-category {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 16px;
  padding: 2rem;
  transition: border-color 0.3s;
}

.tools-category:hover { border-color: var(--border-hover); }

.tools-cat-label {
  font-family: 'DM Mono', monospace;
  font-size: 0.7rem;
  letter-spacing: 0.16em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 0.4rem;
}

.tools-cat-title {
  font-family: 'Syne', sans-serif;
  font-size: 1.25rem;
  font-weight: 700;
  color: var(--text-primary);
  margin-bottom: 1.5rem;
}

.tool-logos { gap: 1rem; }

.tool-item {
  gap: 0.5rem;
  padding: 1rem 0.5rem;
  border-radius: 10px;
  border: 1px solid transparent;
  transition: background 0.2s, border-color 0.2s;
  cursor: default;
}

.tool-item:hover {
  background: var(--accent-dim);
  border-color: var(--border-hover);
}

.tool-item img {
  width: 52px;
  height: 52px;
  object-fit: contain;
  filter: brightness(0.9);
  transition: filter 0.2s, transform 0.2s;
}

.tool-item:hover img {
  filter: brightness(1.1);
  transform: translateY(-3px);
}

.tool-item span {
  font-family: 'DM Mono', monospace;
  font-size: 0.66rem;
  letter-spacing: 0.06em;
  color: var(--text-muted);
  text-align: center;
  transition: color 0.2s;
}

.tool-item:hover span { color: var(--accent); }
</style>

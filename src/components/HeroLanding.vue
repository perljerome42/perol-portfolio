<script setup>
import siteData from '../data/siteData.json'
</script>

<template>
  <section id="landing">
    <div class="container position-relative d-flex">
      <div class="landing-inner">
        <div>
          <div class="tag-line d-inline-flex align-items-center">{{ siteData.hero.tagLine }}</div>
          <h1 class="hero-name">
            <span>{{ siteData.hero.greeting }}</span>I'm <span>{{ siteData.hero.name }}</span>
          </h1>
          <p class="hero-role">{{ siteData.hero.role }}</p>
          <p class="hero-desc">{{ siteData.hero.description }}</p>
          <div class="hero-cta d-flex">
            <a :href="siteData.hero.ctaPrimaryHref" class="btn-primary-custom">{{ siteData.hero.ctaPrimary }}</a>
            <a :href="siteData.hero.ctaSecondaryHref" class="btn-ghost-custom">{{ siteData.hero.ctaSecondary }}</a>
          </div>
        </div>
        <div class="d-flex justify-content-center">
          <div class="portrait-wrap">
            <img :src="siteData.hero.portraitImage" alt="Jerome Portrait">
            <div class="portrait-badge">
              <strong>{{ siteData.hero.badgeYears }}</strong>
              {{ siteData.hero.badgeText }}
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
#landing {
  min-height: 100vh;
  padding-top: var(--nav-height);
  align-items: center;
  position: relative;
  z-index: 1;
}

.landing-inner {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 4rem;
  align-items: center;
  padding: 5rem 0;
}

@media (max-width: 768px) {
  .landing-inner { grid-template-columns: 1fr; text-align: center; }
  .portrait-wrap { order: -1; margin: 0 auto; }
}

.tag-line {
  gap: 0.5rem;
  font-family: 'DM Mono', monospace;
  font-size: 0.72rem;
  letter-spacing: 0.15em;
  text-transform: uppercase;
  color: var(--accent);
  background: var(--accent-dim);
  border: 1px solid var(--border-hover);
  border-radius: 100px;
  padding: 0.35rem 1rem;
  margin-bottom: 1.5rem;
}

.tag-line::before {
  content: '';
  width: 7px; height: 7px;
  background: var(--accent);
  border-radius: 50%;
  animation: pulse 2s infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 1; transform: scale(1); }
  50% { opacity: 0.4; transform: scale(0.8); }
}

.hero-name {
  font-family: 'Syne', sans-serif;
  font-size: clamp(2.8rem, 6vw, 5.5rem);
  font-weight: 800;
  line-height: 1.0;
  letter-spacing: -0.02em;
  color: var(--text-primary);
}

.hero-name span { color: var(--accent); display: block; }

.hero-role {
  font-family: 'DM Mono', monospace;
  font-size: 0.95rem;
  color: var(--text-secondary);
  letter-spacing: 0.05em;
  margin: 1.2rem 0;
}

.hero-desc {
  font-size: 1.05rem;
  color: var(--text-secondary);
  line-height: 1.7;
  max-width: 440px;
}

@media (max-width: 768px) { .hero-desc { margin: 0 auto; } }

.hero-cta {
  margin-top: 2.2rem;
  gap: 1rem;
  flex-wrap: wrap;
}

@media (max-width: 768px) { .hero-cta { justify-content: center; } }

.btn-primary-custom {
  font-family: 'DM Mono', monospace;
  font-size: 0.82rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  background: var(--accent);
  color: #080c10;
  border: none;
  padding: 0.75rem 1.8rem;
  border-radius: 8px;
  cursor: pointer;
  font-weight: 500;
  transition: transform 0.2s, box-shadow 0.2s;
  text-decoration: none;
}

.btn-primary-custom:hover {
  transform: translateY(-2px);
  box-shadow: 0 8px 30px var(--accent-glow);
  color: #080c10;
}

.btn-ghost-custom {
  font-family: 'DM Mono', monospace;
  font-size: 0.82rem;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  background: transparent;
  color: var(--text-secondary);
  border: 1px solid var(--border-hover);
  padding: 0.75rem 1.8rem;
  border-radius: 8px;
  cursor: pointer;
  transition: color 0.2s, border-color 0.2s, transform 0.2s;
  text-decoration: none;
}

.btn-ghost-custom:hover {
  color: var(--accent);
  border-color: var(--accent);
  transform: translateY(-2px);
}

.portrait-wrap {
  position: relative;
  width: 320px;
  height: 380px;
}

.portrait-wrap::before {
  content: '';
  position: absolute;
  inset: -2px;
  border-radius: 28px;
  background: linear-gradient(135deg, var(--accent), transparent 60%);
  z-index: 0;
}

.portrait-wrap::after {
  content: '';
  position: absolute;
  inset: 2px;
  border-radius: 26px;
  background: var(--bg-secondary);
  z-index: 1;
}

.portrait-wrap img {
  position: absolute;
  inset: 2px;
  width: calc(100% - 4px);
  height: calc(100% - 4px);
  object-fit: cover;
  border-radius: 26px;
  z-index: 2;
  filter: grayscale(15%);
}

.portrait-badge {
  position: absolute;
  bottom: -18px;
  right: -18px;
  background: var(--bg-card);
  border: 1px solid var(--border-hover);
  border-radius: 12px;
  padding: 0.7rem 1.1rem;
  z-index: 10;
  font-family: 'DM Mono', monospace;
  font-size: 0.75rem;
  color: var(--accent);
  letter-spacing: 0.05em;
  backdrop-filter: blur(8px);
}

.portrait-badge strong { display: block; font-size: 1.3rem; line-height: 1; }
</style>

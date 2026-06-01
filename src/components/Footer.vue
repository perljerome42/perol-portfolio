<script setup>
import siteData from '../data/siteData.json'
</script>

<template>
  <footer>
    <div class="container">
      <div class="footer-inner d-flex justify-content-center gap-2">
        <span class="footer-name">{{ siteData.footer.name }}</span>
        <span class="footer-copy">{{ siteData.footer.copyright }}</span>
        <span class="footer-copy">{{ siteData.footer.tagline }}</span>
      </div>
    </div>
  </footer>
</template>

<style scoped>
footer {
  background: var(--bg-secondary);
  border-top: 1px solid var(--border);
  padding: 1.8rem 0;
}

.footer-name {
  font-family: 'Syne', sans-serif;
  font-weight: 700;
  color: var(--accent);
  font-size: 0.9rem;
}

.footer-copy {
  font-family: 'DM Mono', monospace;
  font-size: 0.7rem;
  color: var(--text-muted);
  letter-spacing: 0.06em;
}
</style>

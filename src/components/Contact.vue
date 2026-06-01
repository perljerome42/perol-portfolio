<script setup>
import siteData from '../data/siteData.json'
</script>

<template>
  <section id="contact" class="position-relative">
    <div class="container">
      <div class="text-center reveal">
        <p class="section-label">{{ siteData.contact.label }}</p>
        <h2 class="section-title">{{ siteData.contact.title }}</h2>
        <p>{{ siteData.contact.subtitle }}</p>
      </div>
      <div class="contact-inner reveal">
        <form>
          <div class="mb-3" v-for="field in siteData.contact.formFields" :key="field.id">
            <label :for="field.id" class="form-label">{{ field.label }}</label>
            <textarea v-if="field.type === 'textarea'" class="form-control" :id="field.id" :placeholder="field.placeholder" :rows="field.rows || 5"></textarea>
            <input v-else :type="field.type" class="form-control" :id="field.id" :placeholder="field.placeholder">
          </div>
          <div class="contact-footer d-flex flex-wrap align-items-center justify-content-between">
            <div class="social-links d-flex">
              <a v-for="social in siteData.contact.socialLinks" :key="social.platform" :href="social.href" target="_blank" class="social-link d-flex justify-content-center align-items-center">
                <i :class="social.icon"></i>
              </a>
            </div>
            <button type="submit" class="btn-primary-custom">{{ siteData.contact.submitButtonText }}</button>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<style scoped>
#contact {
  padding: 7rem 0;
  z-index: 1;
}

#contact > .container > .text-center > p {
  color: var(--text-secondary);
  margin-top: 0.8rem;
  font-size: 0.95rem;
}

.contact-inner {
  margin-top: 3rem;
  max-width: 680px;
  margin-left: auto;
  margin-right: auto;
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: 20px;
  padding: 3rem;
}

.contact-inner:hover { border-color: var(--border-hover); }

@media (max-width: 768px) {
  .contact-inner { padding: 2rem 1.5rem; }
}

.form-label {
  font-family: 'DM Mono', monospace;
  font-size: 0.72rem;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--text-secondary);
  margin-bottom: 0.5rem;
}

.form-control {
  background: var(--bg-secondary) !important;
  border: 1px solid var(--border) !important;
  border-radius: 10px !important;
  color: var(--text-primary) !important;
  font-family: 'DM Sans', sans-serif;
  font-size: 0.92rem;
  padding: 0.75rem 1rem;
  transition: border-color 0.2s, box-shadow 0.2s;
}

.form-control:focus {
  border-color: var(--accent) !important;
  box-shadow: 0 0 0 3px var(--accent-dim) !important;
  outline: none;
}

.form-control::placeholder { color: var(--text-muted) !important; }

textarea.form-control { resize: vertical; min-height: 130px; }

.contact-footer {
  margin-top: 1.8rem;
  gap: 1rem;
}

.social-links { gap: 0.75rem; }

.social-link {
  width: 40px;
  height: 40px;
  border-radius: 8px;
  border: 1px solid var(--border);
  color: var(--text-secondary) !important;
  font-size: 1rem;
  transition: color 0.2s, border-color 0.2s, background 0.2s, transform 0.2s;
  text-decoration: none;
}

.social-link:hover {
  color: var(--accent) !important;
  border-color: var(--border-hover);
  background: var(--accent-dim);
  transform: translateY(-2px);
}

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
</style>

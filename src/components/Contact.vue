<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { Notyf } from 'notyf'
import 'notyf/notyf.min.css'

const notyf = new Notyf()

const name = ref('')
const email = ref('')
const message = ref('')
const isLoading = ref(false)

const WEB3FORMS_ACCESS_KEY = 'c50892be-4c78-4071-988f-1bf685aae888'
const subject = 'New message from Portfolio Contact Form'

/* reCAPTCHA */
const SITE_KEY = '6Lc-SgctAAAAAOPGCenmxH91uLxTVAO1ymBttsTK'
const recaptchaContainer = ref(null)
const recaptchaWidgetId = ref(null)
const recaptchaToken = ref('')

function onRecaptchaSuccess(token) {
  recaptchaToken.value = token
}

function onRecaptchaExpired() {
  recaptchaToken.value = ''
}

function renderRecaptcha() {
  if (!window.grecaptcha) {
    console.error('reCAPTCHA not loaded')
    return
  }
  recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
    sitekey: SITE_KEY,
    size: 'normal',
    callback: onRecaptchaSuccess,
    'expired-callback': onRecaptchaExpired
  })
}

function resetRecaptcha() {
  if (recaptchaWidgetId.value !== null) {
    window.grecaptcha.reset(recaptchaWidgetId.value)
    recaptchaToken.value = ''
  }
}

const submitForm = async () => {
  if (!recaptchaToken.value) {
    notyf.error('Please verify you are a human')
    return
  }

  isLoading.value = true

  try {
    const response = await fetch('https://api.web3forms.com/submit', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
        Accept: 'application/json'
      },
      body: JSON.stringify({
        access_key: WEB3FORMS_ACCESS_KEY,
        subject: subject,
        name: name.value,
        email: email.value,
        message: message.value
      })
    })

    const result = await response.json()

    if (result.success) {
      notyf.success('Message sent!')
      name.value = ''
      email.value = ''
      message.value = ''
    } else {
      notyf.error('Failed to send message')
    }
  } catch (error) {
    console.log(error)
    notyf.error('Failed to send message')
  } finally {
    isLoading.value = false
    resetRecaptcha()
  }
}

onMounted(() => {
  const interval = setInterval(() => {
    if (window.grecaptcha && window.grecaptcha.render) {
      renderRecaptcha()
      clearInterval(interval)
    }
  }, 100)

  onBeforeUnmount(() => {
    clearInterval(interval)
  })
})
</script>

<template>
  <section id="contact" class="position-relative">
    <div class="container">
      <div class="text-center reveal">
        <p class="section-label">// Get in Touch</p>
        <h2 class="section-title">Let's Work Together</h2>
        <p>Have a project in mind? Send me a message.</p>
      </div>
      <div class="contact-inner reveal">
        <form @submit.prevent="submitForm">
          <div class="mb-3">
            <label for="name" class="form-label">Name</label>
            <input type="text" v-model="name" class="form-control" id="name" placeholder="John Doe">
          </div>
          <div class="mb-3">
            <label for="email" class="form-label">Email address</label>
            <input type="email" v-model="email" class="form-control" id="email" placeholder="john.doe@email.com">
          </div>
          <div class="mb-3">
            <label for="message" class="form-label">Message</label>
            <textarea v-model="message" class="form-control" id="message" rows="5" placeholder="Tell me about your project..."></textarea>
          </div>
          <div class="contact-footer d-flex flex-wrap align-items-center justify-content-between">
            <div class="social-links d-flex">
              <a href="https://github.com/yourusername" target="_blank" class="social-link d-flex justify-content-center align-items-center">
                <i class="fa-brands fa-github"></i>
              </a>
              <a href="https://linkedin.com/in/yourusername" target="_blank" class="social-link d-flex justify-content-center align-items-center">
                <i class="fa-brands fa-linkedin"></i>
              </a>
              <a href="https://gitlab.com/yourusername" target="_blank" class="social-link d-flex justify-content-center align-items-center">
                <i class="fa-brands fa-gitlab"></i>
              </a>
            </div>
            <button type="submit" class="btn-primary-custom" :disabled="isLoading">{{ isLoading ? 'Sending...' : 'Send Message' }}</button>
          </div>
          <div class="d-flex justify-content-end mt-2">
            <div ref="recaptchaContainer"></div>
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

.btn-primary-custom:disabled {
  opacity: 0.6;
  cursor: not-allowed;
  transform: none;
}
</style>

<script setup>
import Navbar from './components/Navbar.vue'
import HeroLanding from './components/HeroLanding.vue'
import Projects from './components/Projects.vue'
import Tools from './components/Tools.vue'
import Contact from './components/Contact.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div class="ambient ambient-1"></div>
  <div class="ambient ambient-2"></div>
  <Navbar />
  <main>
    <HeroLanding />
    <Projects />
    <Tools />
    <Contact />
  </main>
  <Footer />
</template>

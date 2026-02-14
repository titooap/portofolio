<script setup>
import { onMounted } from 'vue'
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import ExperienceSection from './components/ExperienceSection.vue'
import EducationSection from './components/EducationSection.vue'
import ContactSection from './components/ContactSection.vue'

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('revealed')
        }
      })
    },
    { threshold: 0.15 }
  )

  document.querySelectorAll('.reveal').forEach((el) => {
    observer.observe(el)
  })
})
</script>

<template>
  <NavBar />
  <main>
    <HeroSection />
    <AboutSection />
    <SkillsSection />
    <ExperienceSection />
    <EducationSection />
    <ContactSection />
  </main>
</template>

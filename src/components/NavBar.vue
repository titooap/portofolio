<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const scrolled = ref(false)
const menuOpen = ref(false)
const activeSection = ref('about')

const navLinks = [
  { label: 'About', href: '#about' },
  { label: 'Skills', href: '#skills' },
  { label: 'Experience', href: '#experience' },
  { label: 'Education', href: '#education' },
  { label: 'Contact', href: '#contact' },
]

function handleScroll() {
  scrolled.value = window.scrollY > 100

  const sections = navLinks.map(link => link.href.substring(1))
  for (let i = sections.length - 1; i >= 0; i--) {
    const el = document.getElementById(sections[i])
    if (el) {
      const rect = el.getBoundingClientRect()
      if (rect.top <= 150) {
        activeSection.value = sections[i]
        break
      }
    }
  }
}

function toggleMenu() {
  menuOpen.value = !menuOpen.value
  document.body.style.overflow = menuOpen.value ? 'hidden' : ''
}

function closeMenu() {
  menuOpen.value = false
  document.body.style.overflow = ''
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll, { passive: true })
  handleScroll()
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
  document.body.style.overflow = ''
})
</script>

<template>
  <nav class="navbar" :class="{ scrolled }">
    <!-- Top-edge glass reflection line -->
    <div class="navbar__reflection" />

    <div class="navbar__inner">
      <ul class="navbar__links">
        <li v-for="link in navLinks" :key="link.href">
          <a
            :href="link.href"
            class="navbar__link"
            :class="{ active: activeSection === link.href.substring(1) }"
          >
            {{ link.label }}
          </a>
        </li>
      </ul>

      <button
        class="navbar__hamburger"
        :class="{ open: menuOpen }"
        @click="toggleMenu"
        aria-label="Toggle menu"
      >
        <span></span>
        <span></span>
        <span></span>
      </button>
    </div>

    <Transition name="overlay">
      <div v-if="menuOpen" class="navbar__overlay" @click.self="closeMenu">
        <ul class="navbar__overlay-links">
          <li
            v-for="(link, index) in navLinks"
            :key="link.href"
            :style="{ animationDelay: `${index * 0.08 + 0.12}s` }"
          >
            <a
              :href="link.href"
              class="navbar__overlay-link"
              :class="{ active: activeSection === link.href.substring(1) }"
              @click="closeMenu"
            >
              {{ link.label }}
            </a>
          </li>
        </ul>
      </div>
    </Transition>
  </nav>
</template>

<style scoped>
/* ───────────────────────────────────────────
   NAVBAR — Liquid Glass
   ─────────────────────────────────────────── */
.navbar {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  padding: 18px 32px;
  background: transparent;
  border-bottom: 1px solid transparent;
  transition:
    background var(--transition-medium) var(--ease-out-expo),
    border-color var(--transition-medium) var(--ease-out-expo),
    backdrop-filter var(--transition-medium) var(--ease-out-expo),
    box-shadow var(--transition-medium) var(--ease-out-expo);
}

.navbar.scrolled {
  background: var(--glass-light);
  border-bottom-color: var(--glass-border-faint);
  backdrop-filter: blur(var(--blur-md)) saturate(1.3);
  -webkit-backdrop-filter: blur(var(--blur-md)) saturate(1.3);
  box-shadow:
    0 1px 0 0 var(--glass-border-faint),
    0 8px 32px -8px rgba(0, 0, 0, 0.4);
}

/* ── Top-edge glass reflection shimmer ── */
.navbar__reflection {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent 0%,
    var(--glass-border-faint) 15%,
    var(--reflect-glow) 35%,
    var(--glass-border-light) 50%,
    var(--reflect-glow) 65%,
    var(--glass-border-faint) 85%,
    transparent 100%
  );
  opacity: 0;
  transition: opacity var(--transition-medium) var(--ease-out-expo);
  pointer-events: none;
}

.navbar.scrolled .navbar__reflection {
  opacity: 1;
}

/* ── Inner layout ── */
.navbar__inner {
  display: flex;
  align-items: center;
  justify-content: center;
  max-width: 1200px;
  margin: 0 auto;
}

/* ── Desktop links ── */
.navbar__links {
  display: flex;
  list-style: none;
  gap: 32px;
  margin: 0;
  padding: 0;
}

.navbar__link {
  font-family: var(--font-body);
  font-size: 0.72rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 2px;
  color: var(--text-secondary);
  text-decoration: none;
  position: relative;
  padding-bottom: 4px;
  transition:
    color var(--transition-fast) var(--ease-out-expo),
    text-shadow var(--transition-fast) var(--ease-out-expo);
}

.navbar__link::after {
  content: '';
  position: absolute;
  bottom: 0;
  left: 50%;
  width: 0;
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent,
    var(--accent),
    transparent
  );
  transition: width var(--transition-fast) var(--ease-out-expo),
              left var(--transition-fast) var(--ease-out-expo);
}

.navbar__link:hover,
.navbar__link.active {
  color: var(--accent);
  text-shadow: 0 0 16px var(--accent-glow);
}

.navbar__link:hover::after,
.navbar__link.active::after {
  width: 100%;
  left: 0;
}

/* ── Hamburger ── */
.navbar__hamburger {
  display: none;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 5px;
  width: 36px;
  height: 36px;
  background: none;
  border: 1px solid transparent;
  border-radius: 8px;
  cursor: pointer;
  padding: 0;
  z-index: 101;
  transition:
    border-color var(--transition-fast) var(--ease-out-expo),
    background var(--transition-fast) var(--ease-out-expo);
}

.navbar__hamburger:hover {
  border-color: var(--glass-border-faint);
  background: var(--glass-thin);
}

.navbar__hamburger span {
  display: block;
  width: 22px;
  height: 1.5px;
  background: var(--text-primary);
  border-radius: 2px;
  transition:
    transform var(--transition-medium) var(--ease-spring),
    opacity var(--transition-fast) var(--ease-out-expo),
    background var(--transition-fast) var(--ease-out-expo),
    width var(--transition-fast) var(--ease-out-expo);
  transform-origin: center;
}

.navbar__hamburger.open span:nth-child(1) {
  transform: translateY(7px) rotate(45deg);
  background: var(--accent);
}

.navbar__hamburger.open span:nth-child(2) {
  opacity: 0;
  width: 0;
}

.navbar__hamburger.open span:nth-child(3) {
  transform: translateY(-7px) rotate(-45deg);
  background: var(--accent);
}

/* ── Full-screen frosted overlay ── */
.navbar__overlay {
  position: fixed;
  inset: 0;
  z-index: 99;
  background: var(--glass-medium);
  display: flex;
  align-items: center;
  justify-content: center;
  backdrop-filter: blur(var(--blur-lg)) saturate(1.4);
  -webkit-backdrop-filter: blur(var(--blur-lg)) saturate(1.4);
}

.navbar__overlay::before {
  content: '';
  position: absolute;
  inset: 0;
  background: radial-gradient(
    ellipse at 50% 30%,
    var(--accent-glass) 0%,
    transparent 60%
  );
  pointer-events: none;
}

.navbar__overlay-links {
  list-style: none;
  padding: 0;
  margin: 0;
  text-align: center;
  display: flex;
  flex-direction: column;
  gap: 32px;
  position: relative;
  z-index: 1;
}

.navbar__overlay-links li {
  opacity: 0;
  transform: translateY(24px) scale(0.96);
  animation: glassSlideIn 0.5s var(--ease-out-expo) forwards;
}

@keyframes glassSlideIn {
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

.navbar__overlay-link {
  font-family: var(--font-heading);
  font-size: 2rem;
  font-weight: 600;
  text-transform: uppercase;
  letter-spacing: 6px;
  color: var(--text-secondary);
  text-decoration: none;
  position: relative;
  padding: 8px 24px;
  border-radius: 12px;
  transition:
    color var(--transition-fast) var(--ease-out-expo),
    text-shadow var(--transition-fast) var(--ease-out-expo),
    background var(--transition-fast) var(--ease-out-expo);
}

.navbar__overlay-link:hover {
  color: var(--accent);
  text-shadow: 0 0 24px var(--accent-glow);
  background: var(--glass-thin);
}

.navbar__overlay-link.active {
  color: var(--accent);
  text-shadow: 0 0 20px var(--accent-glow);
}

.navbar__overlay-link.active::before {
  content: '';
  position: absolute;
  left: -8px;
  top: 50%;
  transform: translateY(-50%);
  width: 6px;
  height: 6px;
  background: var(--accent);
  border-radius: 50%;
  box-shadow:
    0 0 8px var(--accent-glow),
    0 0 20px rgba(212, 168, 67, 0.15);
}

/* ── Overlay transitions ── */
.overlay-enter-active {
  transition: opacity var(--transition-medium) var(--ease-out-expo);
}

.overlay-leave-active {
  transition: opacity var(--transition-fast) var(--ease-out-expo);
}

.overlay-enter-from,
.overlay-leave-to {
  opacity: 0;
}

.overlay-enter-from .navbar__overlay-links li {
  opacity: 0;
  transform: translateY(24px) scale(0.96);
}

/* ── Mobile ── */
@media (max-width: 767px) {
  .navbar {
    padding: 18px 20px;
  }

  .navbar__links {
    display: none;
  }

  .navbar__hamburger {
    display: flex;
  }
}
</style>

<script setup>
import { ref, onMounted } from 'vue'
import heroBg from '../assets/hero-bg.jpg'

const visible = ref(false)

onMounted(() => {
  requestAnimationFrame(() => {
    visible.value = true
  })
})
</script>

<template>
  <section id="hero" class="hero" :style="{ backgroundImage: `url(${heroBg})` }">
    <!-- Atmosphere -->
    <div class="hero__overlay"></div>
    <div class="hero__frost"></div>

    <!-- Ambient orbs -->
    <div class="hero__orb hero__orb--gold"></div>
    <div class="hero__orb hero__orb--cool"></div>

    <!-- Content -->
    <div class="hero__content" :class="{ visible }">
      <!-- Floating greeting -->
      <span class="hero__greeting">
        <span class="hero__greeting-dot"></span>
        Hello, I'm
      </span>

      <!-- Glass bar with name -->
      <div class="hero__bar">
        <div class="hero__bar-shimmer"></div>
        <h1 class="hero__name">TITO ADI PRASETYO</h1>
      </div>

      <!-- Floating tagline -->
      <p class="hero__tagline">
        Information Systems Student
        <span class="hero__sep">//</span>
        Aspiring Web Developer
      </p>

      <!-- Floating CTA -->
      <a href="./cv-tito.pdf" download class="hero__cta">
        <span class="hero__cta-label">Download CV</span>
        <svg width="14" height="14" viewBox="0 0 14 14" fill="none">
          <path d="M7 1.5v8.5M3.5 7L7 10.5 10.5 7" stroke="currentColor" stroke-width="1.2" stroke-linecap="round" stroke-linejoin="round"/>
        </svg>
      </a>
    </div>

    <!-- Scroll capsule -->
    <div class="hero__scroll" :class="{ visible }">
      <div class="hero__scroll-capsule">
        <div class="hero__scroll-dot"></div>
      </div>
      <span class="hero__scroll-label">scroll</span>
    </div>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  width: 100%;
  height: 100vh;
  min-height: 620px;
  display: flex;
  align-items: center;
  justify-content: center;
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  overflow: hidden;
}

/* ── Atmosphere ── */
.hero__overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    180deg,
    rgba(8, 10, 18, 0.25) 0%,
    rgba(11, 13, 23, 0.45) 35%,
    rgba(11, 13, 23, 0.85) 80%,
    rgba(11, 13, 23, 1) 100%
  );
  z-index: 1;
}

.hero__frost {
  position: absolute;
  inset: 0;
  backdrop-filter: blur(1.5px) saturate(1.15);
  -webkit-backdrop-filter: blur(1.5px) saturate(1.15);
  z-index: 2;
}

/* ── Orbs ── */
.hero__orb {
  position: absolute;
  border-radius: 50%;
  pointer-events: none;
  z-index: 3;
}

.hero__orb--gold {
  width: 460px;
  height: 460px;
  background: radial-gradient(circle, rgba(212, 168, 67, 0.08) 0%, transparent 70%);
  top: 25%;
  left: 50%;
  transform: translateX(-50%);
  animation: orbDrift 14s ease-in-out infinite;
}

.hero__orb--cool {
  width: 320px;
  height: 320px;
  background: radial-gradient(circle, rgba(168, 196, 224, 0.05) 0%, transparent 70%);
  top: 15%;
  right: 12%;
  animation: orbDrift 18s ease-in-out infinite reverse;
}

@keyframes orbDrift {
  0%, 100% { transform: translate(0, 0); }
  33% { transform: translate(15px, -10px); }
  66% { transform: translate(-10px, 8px); }
}

/* ── Content ── */
.hero__content {
  position: relative;
  z-index: 5;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0;
  padding: 0 24px;
  width: 100%;
}

/* ── Greeting ── */
.hero__greeting {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 5px 16px;
  background: var(--glass-medium);
  border: 1px solid var(--glass-border-faint);
  border-radius: 100px;
  font-family: var(--font-body);
  font-size: 0.72rem;
  font-weight: 500;
  color: var(--accent);
  text-transform: uppercase;
  letter-spacing: 3px;
  margin-bottom: 24px;
  opacity: 0;
  transform: translateY(14px);
  transition: opacity 0.7s var(--ease-out-expo), transform 0.7s var(--ease-spring);
}

.hero__content.visible .hero__greeting {
  opacity: 1;
  transform: translateY(0);
}

.hero__greeting-dot {
  width: 5px;
  height: 5px;
  background: var(--accent);
  border-radius: 50%;
  box-shadow: 0 0 6px var(--accent-glow);
  animation: pulse 2.8s ease-in-out infinite;
}

@keyframes pulse {
  0%, 100% { opacity: 0.4; transform: scale(0.8); }
  50% { opacity: 1; transform: scale(1.15); }
}

/* ── Glass Bar ── */
.hero__bar {
  position: relative;
  width: min(80%, 800px);
  padding: 14px 0;
  background: var(--glass-light);
  backdrop-filter: var(--blur-md) saturate(1.35);
  -webkit-backdrop-filter: var(--blur-md) saturate(1.35);
  border: 1px solid var(--glass-border-light);
  border-radius: 14px;
  display: flex;
  align-items: center;
  justify-content: center;
  margin-bottom: 28px;
  overflow: hidden;
  box-shadow:
    0 16px 60px rgba(0, 0, 0, 0.35),
    0 0 30px rgba(212, 168, 67, 0.03),
    inset 0 1px 0 rgba(255, 255, 255, 0.05);
  opacity: 0;
  transform: translateY(18px) scaleX(0.95);
  transition: opacity 0.8s var(--ease-out-expo) 0.15s, transform 0.8s var(--ease-spring) 0.15s;
}

.hero__content.visible .hero__bar {
  opacity: 1;
  transform: translateY(0) scaleX(1);
}

.hero__bar-shimmer {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent 0%,
    rgba(255, 255, 255, 0.08) 20%,
    rgba(255, 255, 255, 0.18) 50%,
    rgba(255, 255, 255, 0.08) 80%,
    transparent 100%
  );
  pointer-events: none;
}

/* ── Name ── */
.hero__name {
  font-family: var(--font-heading);
  font-size: clamp(2rem, 5.5vw, 4.2rem);
  font-weight: 700;
  color: var(--text-primary);
  letter-spacing: -0.015em;
  line-height: 1;
  text-align: center;
  white-space: nowrap;
  text-shadow: 0 0 50px rgba(212, 168, 67, 0.06);
  padding: 0 32px;
}

/* ── Tagline ── */
.hero__tagline {
  font-family: var(--font-body);
  font-size: 0.88rem;
  font-weight: 400;
  color: var(--text-secondary);
  letter-spacing: 0.3px;
  text-align: center;
  margin-bottom: 36px;
  opacity: 0;
  transform: translateY(12px);
  transition: opacity 0.7s var(--ease-out-expo) 0.4s, transform 0.7s var(--ease-spring) 0.4s;
}

.hero__content.visible .hero__tagline {
  opacity: 1;
  transform: translateY(0);
}

.hero__sep {
  display: inline-block;
  margin: 0 10px;
  color: var(--accent-dim);
  font-weight: 300;
  opacity: 0.5;
}

/* ── CTA ── */
.hero__cta {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  padding: 11px 30px;
  background: var(--glass-medium);
  border: 1px solid var(--glass-border-light);
  border-radius: 100px;
  color: var(--accent);
  font-family: var(--font-body);
  font-size: 0.74rem;
  font-weight: 500;
  text-transform: uppercase;
  letter-spacing: 2px;
  text-decoration: none;
  position: relative;
  overflow: hidden;
  opacity: 0;
  transform: translateY(12px);
  transition:
    opacity 0.7s var(--ease-out-expo) 0.6s,
    transform 0.7s var(--ease-spring) 0.6s,
    background 0.3s var(--ease-out-expo),
    border-color 0.3s var(--ease-out-expo),
    box-shadow 0.4s var(--ease-out-expo),
    color 0.3s var(--ease-out-expo);
}

.hero__content.visible .hero__cta {
  opacity: 1;
  transform: translateY(0);
}

.hero__cta::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 50%;
  background: linear-gradient(to bottom, rgba(255, 255, 255, 0.03), transparent);
  border-radius: 100px 100px 0 0;
  pointer-events: none;
}

.hero__cta:hover {
  background: var(--accent-glass);
  border-color: rgba(212, 168, 67, 0.25);
  box-shadow: 0 4px 20px rgba(212, 168, 67, 0.12);
  color: var(--accent-light);
}

.hero__cta svg {
  transition: transform 0.3s var(--ease-out-expo);
}

.hero__cta:hover svg {
  transform: translateY(2px);
}

/* ── Scroll capsule ── */
.hero__scroll {
  position: absolute;
  bottom: 36px;
  left: 50%;
  transform: translateX(-50%);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 8px;
  z-index: 5;
  opacity: 0;
  transition: opacity 1s var(--ease-out-expo) 1.2s;
}

.hero__scroll.visible {
  opacity: 1;
}

.hero__scroll-capsule {
  width: 18px;
  height: 32px;
  border: 1px solid var(--glass-border-light);
  border-radius: 9px;
  background: var(--glass-thin);
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  display: flex;
  justify-content: center;
  padding-top: 5px;
  position: relative;
  overflow: hidden;
}

.hero__scroll-capsule::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 45%;
  background: linear-gradient(to bottom, rgba(255, 255, 255, 0.03), transparent);
  border-radius: 9px 9px 0 0;
  pointer-events: none;
}

.hero__scroll-dot {
  width: 2.5px;
  height: 7px;
  background: var(--accent);
  border-radius: 2px;
  box-shadow: 0 0 5px var(--accent-glow);
  animation: dropScroll 2s var(--ease-out-expo) infinite;
}

@keyframes dropScroll {
  0% { transform: translateY(0); opacity: 1; }
  100% { transform: translateY(14px); opacity: 0; }
}

.hero__scroll-label {
  font-family: var(--font-body);
  font-size: 0.55rem;
  font-weight: 500;
  color: var(--text-muted);
  text-transform: uppercase;
  letter-spacing: 3px;
}

/* ── Responsive ── */
@media (max-width: 768px) {
  .hero__bar {
    width: 92%;
    padding: 12px 0;
    border-radius: 12px;
  }

  .hero__name {
    white-space: normal;
    padding: 0 20px;
    font-size: clamp(1.8rem, 7vw, 2.8rem);
  }

  .hero__orb--cool { display: none; }

  .hero__tagline {
    font-size: 0.82rem;
  }

  .hero__sep { display: none; }

  .hero__tagline {
    display: flex;
    flex-direction: column;
    gap: 2px;
  }
}

@media (max-width: 480px) {
  .hero__greeting {
    font-size: 0.65rem;
    letter-spacing: 2px;
  }

  .hero__bar {
    padding: 10px 0;
  }

  .hero__cta {
    padding: 10px 24px;
    font-size: 0.68rem;
  }
}
</style>

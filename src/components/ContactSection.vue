<script setup>
import { ref } from 'vue'

const contacts = ref([
  {
    label: 'titoadi50@gmail.com',
    href: 'mailto:titoadi50@gmail.com',
    icon: 'email'
  },
  {
    label: '085716276819',
    href: 'tel:085716276819',
    icon: 'phone'
  },
  {
    label: 'github.com/titooap',
    href: 'https://github.com/titooap',
    icon: 'github'
  },
  {
    label: 'Previous Portfolio',
    href: 'https://titooap.github.io/Portofolio_UTS/',
    icon: 'portfolio'
  }
])
</script>

<template>
  <section id="contact" class="contact reveal">
    <div class="container">
      <h2 class="section-title section-title--centered">Let's Connect</h2>

      <div class="contact__panel">
        <a
          v-for="(item, index) in contacts"
          :key="index"
          :href="item.href"
          class="contact__item"
          target="_blank"
          rel="noopener noreferrer"
        >
          <!-- Email icon -->
          <svg v-if="item.icon === 'email'" class="contact__icon" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
            <rect x="2" y="4" width="20" height="16" rx="2" />
            <polyline points="22,4 12,13 2,4" />
          </svg>

          <!-- Phone icon -->
          <svg v-else-if="item.icon === 'phone'" class="contact__icon" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
            <path d="M22 16.92v3a2 2 0 0 1-2.18 2 19.79 19.79 0 0 1-8.63-3.07 19.5 19.5 0 0 1-6-6 19.79 19.79 0 0 1-3.07-8.67A2 2 0 0 1 4.11 2h3a2 2 0 0 1 2 1.72 12.84 12.84 0 0 0 .7 2.81 2 2 0 0 1-.45 2.11L8.09 9.91a16 16 0 0 0 6 6l1.27-1.27a2 2 0 0 1 2.11-.45 12.84 12.84 0 0 0 2.81.7A2 2 0 0 1 22 16.92z" />
          </svg>

          <!-- GitHub / Code brackets icon -->
          <svg v-else-if="item.icon === 'github'" class="contact__icon" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
            <polyline points="16 18 22 12 16 6" />
            <polyline points="8 6 2 12 8 18" />
            <line x1="14" y1="4" x2="10" y2="20" />
          </svg>

          <!-- Portfolio / Globe icon -->
          <svg v-else-if="item.icon === 'portfolio'" class="contact__icon" width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.5" stroke-linecap="round" stroke-linejoin="round">
            <circle cx="12" cy="12" r="10" />
            <ellipse cx="12" cy="12" rx="4" ry="10" />
            <line x1="2" y1="12" x2="22" y2="12" />
          </svg>

          <span class="contact__label">{{ item.label }}</span>
        </a>
      </div>

      <div class="contact__cta">
        <a href="./cv-tito.pdf" download class="contact__btn">
          Download CV
        </a>
      </div>

      <footer class="contact__footer">
        <p>&copy; 2026 Tito Adi Prasetyo. Built with Vue.js</p>
      </footer>
    </div>
  </section>
</template>

<style scoped>
.contact {
  background: var(--bg-primary);
  padding: var(--section-padding);
  padding-bottom: 40px;
}

.section-title--centered {
  display: block;
  text-align: center;
}

.section-title--centered::after {
  left: 50%;
  transform: translateX(-50%);
}

/* Glass panel container */
.contact__panel {
  position: relative;
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  gap: 24px;
  margin: 48px auto 0;
  max-width: 500px;
  padding: 48px;
  background: var(--glass-light);
  border: 1px solid var(--glass-border-light);
  border-radius: 20px;
  backdrop-filter: var(--blur-md) saturate(1.4);
  -webkit-backdrop-filter: var(--blur-md) saturate(1.4);
  overflow: hidden;
}

/* Top-edge shimmer on panel */
.contact__panel::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent 0%,
    rgba(255, 255, 255, 0.2) 30%,
    rgba(255, 255, 255, 0.35) 50%,
    rgba(255, 255, 255, 0.2) 70%,
    transparent 100%
  );
}

/* Soft ambient glow behind panel */
.contact__panel::after {
  content: '';
  position: absolute;
  top: -30px;
  left: -30px;
  right: -30px;
  bottom: -30px;
  background: radial-gradient(
    ellipse at 50% 0%,
    var(--accent-glow) 0%,
    transparent 70%
  );
  z-index: -1;
  opacity: 0.25;
  pointer-events: none;
}

.contact__item {
  display: flex;
  align-items: center;
  gap: 14px;
  text-decoration: none;
  color: var(--text-secondary);
  font-family: var(--font-body);
  font-size: 0.95rem;
  transition: color var(--transition-fast);
}

.contact__item:hover {
  color: var(--accent);
}

.contact__icon {
  color: var(--accent-dim);
  flex-shrink: 0;
  transition:
    color var(--transition-fast),
    filter var(--transition-fast);
}

.contact__item:hover .contact__icon {
  color: var(--accent);
  filter: drop-shadow(0 0 6px var(--accent-glow));
}

.contact__label {
  line-height: 1;
}

.contact__cta {
  display: flex;
  justify-content: center;
  margin-top: 48px;
}

/* Glass download button */
.contact__btn {
  display: inline-block;
  background: var(--glass-medium);
  border: 1px solid var(--glass-border-light);
  border-radius: 100px;
  color: var(--accent);
  padding: 14px 36px;
  font-family: var(--font-body);
  font-size: 0.85rem;
  text-transform: uppercase;
  letter-spacing: 2px;
  text-decoration: none;
  cursor: pointer;
  backdrop-filter: var(--blur-sm);
  -webkit-backdrop-filter: var(--blur-sm);
  transition:
    background var(--transition-fast),
    border-color var(--transition-fast),
    box-shadow var(--transition-fast);
}

.contact__btn:hover {
  background: var(--accent-glass);
  border-color: var(--accent-dim);
  box-shadow: 0 0 20px var(--accent-glow);
}

.contact__footer {
  text-align: center;
  margin-top: 80px;
  padding-top: 20px;
  border-top: 1px solid var(--glass-border-faint);
}

.contact__footer p {
  font-family: var(--font-body);
  font-size: 0.78rem;
  color: var(--text-muted);
  margin: 0;
}
</style>

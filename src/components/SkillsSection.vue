<script setup>
import { ref, reactive, onMounted, onUnmounted } from 'vue'

const sectionRef = ref(null)
const revealed = ref(false)

const skills = reactive([
  {
    name: 'Microsoft Office',
    desc: 'Word, Excel, PowerPoint',
    level: 85,
    icon: 'briefcase',
  },
  {
    name: 'Google Sheets',
    desc: 'Data management & formulas',
    level: 80,
    icon: 'table',
  },
  {
    name: 'Google Colab',
    desc: 'Python notebooks & collaboration',
    level: 70,
    icon: 'terminal',
  },
  {
    name: 'Canva',
    desc: 'Graphic design & presentations',
    level: 85,
    icon: 'palette',
  },
  {
    name: 'Programming',
    desc: 'HTML, CSS, JavaScript',
    level: 65,
    icon: 'code',
  },
  {
    name: 'Figma',
    desc: 'UI/UX design basics',
    level: 60,
    icon: 'layout',
  },
])

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((entry) => {
        if (entry.isIntersecting) {
          entry.target.classList.add('revealed')
          revealed.value = true
        }
      })
    },
    { threshold: 0.15 }
  )

  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }

  onUnmounted(() => observer.disconnect())
})
</script>

<template>
  <section id="skills" ref="sectionRef" class="skills reveal">
    <!-- Ambient glow orb -->
    <div class="skills__glow-orb"></div>

    <div class="container">
      <h2 class="section-title">Technical Skills</h2>

      <div class="skills__grid">
        <div
          v-for="(skill, index) in skills"
          :key="skill.name"
          class="skills__card"
          :style="{ transitionDelay: `${index * 0.08}s` }"
        >
          <!-- Icon -->
          <div class="skills__icon">
            <!-- Briefcase -->
            <svg v-if="skill.icon === 'briefcase'" width="32" height="32" viewBox="0 0 32 32" fill="none">
              <rect x="4" y="12" width="24" height="14" rx="2" stroke="currentColor" stroke-width="1.5"/>
              <path d="M12 12V9a2 2 0 0 1 2-2h4a2 2 0 0 1 2 2v3" stroke="currentColor" stroke-width="1.5"/>
              <line x1="4" y1="19" x2="28" y2="19" stroke="currentColor" stroke-width="1.5" opacity="0.5"/>
            </svg>

            <!-- Table / Grid -->
            <svg v-else-if="skill.icon === 'table'" width="32" height="32" viewBox="0 0 32 32" fill="none">
              <rect x="5" y="6" width="22" height="20" rx="2" stroke="currentColor" stroke-width="1.5"/>
              <line x1="5" y1="12" x2="27" y2="12" stroke="currentColor" stroke-width="1.5"/>
              <line x1="5" y1="18" x2="27" y2="18" stroke="currentColor" stroke-width="1.5"/>
              <line x1="14" y1="12" x2="14" y2="26" stroke="currentColor" stroke-width="1.5"/>
            </svg>

            <!-- Terminal -->
            <svg v-else-if="skill.icon === 'terminal'" width="32" height="32" viewBox="0 0 32 32" fill="none">
              <rect x="4" y="7" width="24" height="18" rx="2" stroke="currentColor" stroke-width="1.5"/>
              <polyline points="9,14 13,17 9,20" stroke="currentColor" stroke-width="1.5" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
              <line x1="16" y1="20" x2="22" y2="20" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            </svg>

            <!-- Palette -->
            <svg v-else-if="skill.icon === 'palette'" width="32" height="32" viewBox="0 0 32 32" fill="none">
              <circle cx="16" cy="16" r="11" stroke="currentColor" stroke-width="1.5"/>
              <circle cx="12" cy="12" r="2" fill="currentColor" opacity="0.6"/>
              <circle cx="20" cy="12" r="2" fill="currentColor" opacity="0.4"/>
              <circle cx="11" cy="18" r="2" fill="currentColor" opacity="0.8"/>
              <path d="M20 17c1.5 0 3 1.2 3 3s-1.5 3-3 3c-1 0-2-.5-2-2 0-1.5 1-2 2-2z" fill="currentColor" opacity="0.5"/>
            </svg>

            <!-- Code brackets -->
            <svg v-else-if="skill.icon === 'code'" width="32" height="32" viewBox="0 0 32 32" fill="none">
              <polyline points="11,10 5,16 11,22" stroke="currentColor" stroke-width="1.5" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
              <polyline points="21,10 27,16 21,22" stroke="currentColor" stroke-width="1.5" fill="none" stroke-linecap="round" stroke-linejoin="round"/>
              <line x1="18" y1="8" x2="14" y2="24" stroke="currentColor" stroke-width="1.5" stroke-linecap="round"/>
            </svg>

            <!-- Layout -->
            <svg v-else-if="skill.icon === 'layout'" width="32" height="32" viewBox="0 0 32 32" fill="none">
              <rect x="5" y="6" width="22" height="20" rx="2" stroke="currentColor" stroke-width="1.5"/>
              <line x1="5" y1="12" x2="27" y2="12" stroke="currentColor" stroke-width="1.5"/>
              <line x1="14" y1="12" x2="14" y2="26" stroke="currentColor" stroke-width="1.5"/>
            </svg>
          </div>

          <!-- Text -->
          <h3 class="skills__name">{{ skill.name }}</h3>
          <p class="skills__desc">{{ skill.desc }}</p>

          <!-- Level bar -->
          <div class="skills__bar-track">
            <div
              class="skills__bar-fill"
              :style="{
                width: revealed ? `${skill.level}%` : '0%',
                transitionDelay: `${index * 0.08 + 0.3}s`,
              }"
            ></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.skills {
  position: relative;
  padding: var(--section-padding);
  background: var(--bg-secondary);
  overflow: hidden;
}

/* ── Ambient glow orb ── */
.skills__glow-orb {
  position: absolute;
  bottom: -100px;
  left: -140px;
  width: 480px;
  height: 480px;
  background: radial-gradient(circle, var(--reflect-glow) 0%, transparent 70%);
  filter: blur(80px);
  pointer-events: none;
  z-index: 0;
  opacity: 0.7;
}

/* ── Grid ── */
.skills__grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
  position: relative;
  z-index: 1;
}

/* ── Card ── */
.skills__card {
  position: relative;
  background: rgba(255, 255, 255, var(--glass-medium));
  border: 1px solid rgba(255, 255, 255, var(--glass-border-faint));
  border-radius: 12px;
  backdrop-filter: blur(var(--blur-sm));
  -webkit-backdrop-filter: blur(var(--blur-sm));
  padding: 24px;
  display: flex;
  flex-direction: column;
  overflow: hidden;
  transition:
    border-color var(--transition-fast),
    box-shadow var(--transition-medium),
    transform var(--transition-fast),
    opacity 0.6s var(--ease-out-expo),
    translate 0.6s var(--ease-out-expo);
  opacity: 0;
  translate: 0 24px;
}

/* Top-edge shimmer reflection */
.skills__card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.14),
    rgba(255, 255, 255, 0.06),
    transparent
  );
  pointer-events: none;
  transition: opacity var(--transition-fast);
}

/* Revealed state */
.skills.revealed .skills__card {
  opacity: 1;
  translate: 0 0;
}

/* Hover */
.skills__card:hover {
  border-color: rgba(255, 255, 255, var(--glass-border-medium));
  box-shadow: 0 8px 32px var(--accent-glow);
  transform: translateY(-3px);
}

.skills__card:hover::before {
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.22),
    rgba(255, 255, 255, 0.1),
    transparent
  );
}

/* ── Icon ── */
.skills__icon {
  width: 32px;
  height: 32px;
  color: var(--accent-dim);
  margin-bottom: 18px;
}

/* ── Text ── */
.skills__name {
  font-family: var(--font-heading);
  font-size: 1rem;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 6px;
}

.skills__desc {
  font-family: var(--font-body);
  font-size: 0.78rem;
  color: var(--text-muted);
  margin-bottom: 20px;
}

/* ── Level bar ── */
.skills__bar-track {
  width: 100%;
  height: 4px;
  background: rgba(255, 255, 255, var(--glass-thin));
  border-radius: 2px;
  overflow: hidden;
  margin-top: auto;
}

.skills__bar-fill {
  height: 100%;
  width: 0%;
  background: linear-gradient(90deg, var(--accent-dim), var(--accent));
  border-radius: 2px;
  box-shadow: 0 0 8px var(--accent-glow);
  transition: width 1s var(--ease-out-expo);
}

/* ── Responsive ── */
@media (max-width: 1024px) {
  .skills__grid {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (max-width: 768px) {
  .skills__grid {
    grid-template-columns: 1fr;
  }

  .skills__glow-orb {
    width: 280px;
    height: 280px;
    bottom: -60px;
    left: -80px;
  }
}
</style>

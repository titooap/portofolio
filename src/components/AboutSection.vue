<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const sectionRef = ref(null)

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

  if (sectionRef.value) {
    observer.observe(sectionRef.value)
  }

  onUnmounted(() => observer.disconnect())
})
</script>

<template>
  <section id="about" ref="sectionRef" class="about reveal">
    <!-- Ambient glow orb -->
    <div class="about__glow-orb"></div>

    <div class="container">
      <h2 class="section-title">About Me</h2>

      <div class="about__grid">
        <!-- Left column: bio text -->
        <div class="about__bio">
          <p class="about__text">
            High-achieving Information Systems undergraduate (GPA 3.83/4.00)
            with a strong interest in web development and technology management.
            Proven leadership experience as the Chief Executive of a National
            Web 3 Seminar, demonstrating strong organizational and
            problem-solving abilities.
          </p>
          <p class="about__text">
            Eager to launch a career as a Web Developer by leveraging
            foundational programming skills and a proactive mindset. Actively
            involved in faculty-level student activities and continuously
            developing skills in programming and network simulation.
          </p>
        </div>

        <!-- Right column: stat cards -->
        <div class="about__stats">
          <div class="about__card">
            <span class="about__card-value">3.83</span>
            <span class="about__card-label">out of 4.00</span>
          </div>
          <div class="about__card">
            <span class="about__card-value">Computer Science</span>
            <span class="about__card-label">Information Systems</span>
          </div>
          <div class="about__card">
            <span class="about__card-value">Web Development</span>
            <span class="about__card-label">Career Goal</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  position: relative;
  padding: var(--section-padding);
  background: var(--bg-primary);
  overflow: hidden;
}

/* ── Ambient glow orb ── */
.about__glow-orb {
  position: absolute;
  top: -80px;
  right: -120px;
  width: 500px;
  height: 500px;
  background: radial-gradient(circle, var(--accent-glow) 0%, transparent 70%);
  filter: blur(80px);
  pointer-events: none;
  z-index: 0;
  opacity: 0.6;
}

/* ── Grid layout ── */
.about__grid {
  display: grid;
  grid-template-columns: 1fr 0.65fr;
  gap: 48px;
  align-items: start;
  position: relative;
  z-index: 1;
}

/* ── Bio column ── */
.about__bio {
  position: relative;
  padding-left: 24px;
  border-left: 1px solid var(--glass-border-faint);
}

.about__bio::before {
  content: '';
  position: absolute;
  top: 0;
  left: -1px;
  width: 1px;
  height: 0;
  background: linear-gradient(
    to bottom,
    var(--accent),
    var(--accent-dim),
    transparent
  );
  transition: height 1s var(--ease-out-expo) 0.3s;
}

.about.revealed .about__bio::before {
  height: 100%;
}

.about__text {
  font-family: var(--font-body);
  font-size: 1rem;
  color: var(--text-secondary);
  line-height: 1.8;
  margin-bottom: 20px;
}

.about__text:last-child {
  margin-bottom: 0;
}

/* ── Stat cards ── */
.about__stats {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.about__card {
  position: relative;
  background: rgba(255, 255, 255, var(--glass-medium));
  border: 1px solid rgba(255, 255, 255, var(--glass-border-faint));
  border-radius: 12px;
  backdrop-filter: blur(var(--blur-sm));
  -webkit-backdrop-filter: blur(var(--blur-sm));
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 4px;
  opacity: 0;
  transform: translateX(30px);
  transition:
    opacity 0.6s var(--ease-out-expo),
    transform 0.6s var(--ease-out-expo),
    border-color var(--transition-fast),
    box-shadow var(--transition-medium);
  overflow: hidden;
}

/* Top-edge shimmer reflection */
.about__card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: linear-gradient(
    90deg,
    transparent,
    rgba(255, 255, 255, 0.15),
    rgba(255, 255, 255, 0.06),
    transparent
  );
  pointer-events: none;
}

/* Hover glow */
.about__card:hover {
  border-color: rgba(255, 255, 255, var(--glass-border-medium));
  box-shadow: 0 8px 32px rgba(212, 168, 67, 0.08);
}

/* Staggered reveal */
.about.revealed .about__card:nth-child(1) {
  opacity: 1;
  transform: translateX(0);
  transition-delay: 0.2s;
}

.about.revealed .about__card:nth-child(2) {
  opacity: 1;
  transform: translateX(0);
  transition-delay: 0.35s;
}

.about.revealed .about__card:nth-child(3) {
  opacity: 1;
  transform: translateX(0);
  transition-delay: 0.5s;
}

.about__card-value {
  font-family: var(--font-heading);
  font-size: 1.4rem;
  font-weight: 700;
  color: var(--accent);
}

.about__card-label {
  font-family: var(--font-body);
  font-size: 0.78rem;
  color: var(--text-muted);
}

/* ── Responsive ── */
@media (max-width: 768px) {
  .about__grid {
    grid-template-columns: 1fr;
    gap: 36px;
  }

  .about__glow-orb {
    width: 300px;
    height: 300px;
    top: -40px;
    right: -60px;
  }
}
</style>

<script setup>
import { ref } from 'vue'

const experiences = ref([
  {
    title: 'Chief Executive',
    org: 'National Seminar (COMPFAIR) & Anniversary of Faculty of Computer Science',
    period: '2025',
    bullets: [
      'Designed and developed the event concept for a national seminar focused on Web 3, including a technology exhibition',
      'Formed, managed, and supervised the event committee to ensure smooth execution',
      'Held full responsibility for the event\'s success and actively established partnerships with sponsors'
    ]
  },
  {
    title: 'Member & Division Coordinator',
    org: 'Student Association & BEM Committees, Faculty of Computer Science',
    period: 'Ongoing',
    bullets: [
      'Executed all assigned tasks and functions diligently and with full responsibility',
      'Collaborated effectively with team members to achieve the goals of various work programs'
    ]
  }
])
</script>

<template>
  <section id="experience" class="experience reveal">
    <div class="container">
      <h2 class="section-title">Experience</h2>
      <div class="timeline">
        <div
          v-for="(exp, index) in experiences"
          :key="index"
          class="timeline__entry"
        >
          <div class="timeline__dot"></div>
          <div class="timeline__card glass-card">
            <div class="timeline__header">
              <div>
                <h3 class="timeline__title">{{ exp.title }}</h3>
                <p class="timeline__org">{{ exp.org }}</p>
              </div>
              <span class="timeline__period">{{ exp.period }}</span>
            </div>
            <ul class="timeline__bullets">
              <li v-for="(bullet, bIndex) in exp.bullets" :key="bIndex">
                {{ bullet }}
              </li>
            </ul>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.experience {
  background: var(--bg-primary);
  padding: var(--section-padding);
}

.timeline {
  position: relative;
  margin-top: 48px;
  padding-left: 24px;
}

/* Timeline line with glow */
.timeline::before {
  content: '';
  position: absolute;
  left: 5px;
  top: 0;
  bottom: 0;
  width: 2px;
  background: linear-gradient(
    to bottom,
    var(--accent),
    var(--accent-dim),
    transparent
  );
  box-shadow: 0 0 8px var(--accent-glow);
}

.timeline__entry {
  position: relative;
  margin-bottom: 48px;
}

.timeline__entry:last-child {
  margin-bottom: 0;
}

/* Glass diamond dot */
.timeline__dot {
  position: absolute;
  left: -25px;
  top: 6px;
  width: 12px;
  height: 12px;
  background: rgba(255, 255, 255, var(--glass-medium));
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
  border: 1px solid rgba(255, 255, 255, var(--glass-border-medium));
  transform: rotate(45deg);
  z-index: 1;
  box-shadow: 0 0 6px var(--accent-glow), inset 0 0 4px var(--accent-glow);
}

/* Glass content card */
.timeline__card {
  position: relative;
  margin-left: 40px;
  padding: 24px;
  background: rgba(255, 255, 255, var(--glass-medium));
  border: 1px solid rgba(255, 255, 255, var(--glass-border-faint));
  border-radius: 12px;
  backdrop-filter: blur(var(--blur-sm)) saturate(1.4);
  -webkit-backdrop-filter: blur(var(--blur-sm)) saturate(1.4);
  overflow: hidden;
}

/* Top-edge shimmer reflection */
.timeline__card::before {
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

/* Soft ambient glow behind card */
.timeline__card::after {
  content: '';
  position: absolute;
  top: -20px;
  left: -20px;
  right: -20px;
  bottom: -20px;
  background: radial-gradient(
    ellipse at 50% 0%,
    var(--accent-glow) 0%,
    transparent 70%
  );
  z-index: -1;
  opacity: 0.3;
  pointer-events: none;
}

.timeline__header {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  gap: 16px;
  flex-wrap: wrap;
}

.timeline__title {
  font-family: var(--font-heading);
  font-size: 1.1rem;
  font-weight: 600;
  color: var(--text-primary);
  margin: 0 0 4px 0;
}

.timeline__org {
  font-family: var(--font-body);
  font-size: 0.9rem;
  color: var(--accent);
  margin: 0;
}

/* Glass pill period badge */
.timeline__period {
  font-family: var(--font-body);
  font-size: 0.72rem;
  color: var(--accent-dim);
  white-space: nowrap;
  flex-shrink: 0;
  background: rgba(255, 255, 255, var(--glass-medium));
  border: 1px solid rgba(255, 255, 255, var(--glass-border-faint));
  border-radius: 100px;
  padding: 4px 14px;
  backdrop-filter: blur(4px);
  -webkit-backdrop-filter: blur(4px);
}

.timeline__bullets {
  list-style: none;
  padding: 0;
  margin: 16px 0 0 0;
}

.timeline__bullets li {
  position: relative;
  font-family: var(--font-body);
  font-size: 0.88rem;
  color: var(--text-secondary);
  line-height: 1.7;
  padding-left: 20px;
  margin-bottom: 6px;
}

/* Custom glass-dot bullet */
.timeline__bullets li::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0.55em;
  width: 4px;
  height: 4px;
  background: var(--accent-dim);
  border-radius: 1px;
}
</style>

<script setup lang="ts">
import { useReveal } from '../composables/useReveal'

defineProps<{ childName: string; motherName: string }>()

const { el, visible } = useReveal()
</script>

<template>
  <section class="message" ref="el" :class="{ visible }">
    <div class="inner">
      <svg class="floral" viewBox="0 0 120 120" aria-hidden="true">
        <g transform="translate(60,60)">
          <ellipse rx="20" ry="7" fill="var(--rose)" opacity="0.28" transform="rotate(0)"/>
          <ellipse rx="20" ry="7" fill="var(--rose)" opacity="0.28" transform="rotate(40)"/>
          <ellipse rx="20" ry="7" fill="var(--rose)" opacity="0.28" transform="rotate(80)"/>
          <ellipse rx="20" ry="7" fill="var(--rose)" opacity="0.28" transform="rotate(120)"/>
          <ellipse rx="20" ry="7" fill="var(--rose)" opacity="0.28" transform="rotate(160)"/>
          <circle r="6" fill="var(--rose-deep)" opacity="0.45"/>
        </g>
        <g transform="translate(16,28)">
          <ellipse rx="9" ry="3.5" fill="var(--sage)" opacity="0.45" transform="rotate(25)"/>
          <ellipse rx="9" ry="3.5" fill="var(--sage)" opacity="0.45" transform="rotate(65)"/>
          <circle r="3" fill="var(--rose)" opacity="0.5"/>
        </g>
        <g transform="translate(102,85)">
          <ellipse rx="9" ry="3.5" fill="var(--sage)" opacity="0.45" transform="rotate(-20)"/>
          <ellipse rx="9" ry="3.5" fill="var(--sage)" opacity="0.45" transform="rotate(30)"/>
          <circle r="3" fill="var(--rose)" opacity="0.5"/>
        </g>
      </svg>

      <blockquote>
        <p>
          Maman, tu es la plus belle,<br />
          la plus douce, la plus formidable<br />
          de toutes les mamans du monde.
        </p>
        <p>
          Merci pour tous tes câlins,<br />
          tes chansons du soir,<br />
          et ton sourire qui éclaire mes journées.
        </p>
        <p>Je t'aime de tout mon petit cœur.</p>
      </blockquote>

      <footer class="letter-footer">
        <div class="line" />
        <div class="signed">
          <p class="from">Ton {{ childName }}</p>
          <p class="age">2 ans et tout plein d'amour</p>
        </div>
        <div class="line" />
      </footer>
    </div>

    <div class="wave" aria-hidden="true">
      <svg viewBox="0 0 1440 72" preserveAspectRatio="none">
        <path d="M0,36 Q360,72 720,36 Q1080,0 1440,36 L1440,72 L0,72 Z" fill="var(--ivory)"/>
      </svg>
    </div>
  </section>
</template>

<style scoped>
.message {
  position: relative;
  background: linear-gradient(140deg, #F0E8E0, #E8D8D2, #EAE0D8);
  padding: 7rem 2rem 5rem;
  text-align: center;
  opacity: 0;
  transform: translateY(32px);
  transition: opacity 1s ease 0.1s, transform 1s ease 0.1s;
}

.message.visible {
  opacity: 1;
  transform: translateY(0);
}

.inner {
  max-width: 580px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 2.8rem;
}

.floral { width: 104px; height: 104px; }

blockquote {
  font-family: var(--font-display);
  font-size: clamp(1.3rem, 3.5vw, 1.8rem);
  font-style: italic;
  font-weight: 300;
  line-height: 1.85;
  color: var(--text);
  display: flex;
  flex-direction: column;
  gap: 1.6rem;
  border: none;
  padding: 0;
  margin: 0;
}

.letter-footer {
  display: flex;
  align-items: center;
  gap: 2rem;
  width: 100%;
}

.line {
  flex: 1;
  height: 1px;
  background: var(--rose);
  opacity: 0.35;
}

.from {
  font-family: var(--font-display);
  font-size: 1.15rem;
  font-style: italic;
  color: var(--burgundy);
  margin-bottom: 0.2rem;
}

.age {
  font-size: 0.76rem;
  letter-spacing: 0.16em;
  color: var(--text-muted);
  text-transform: uppercase;
}

.wave {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  line-height: 0;
}

.wave svg { width: 100%; height: 72px; display: block; }
</style>
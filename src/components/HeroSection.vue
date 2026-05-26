<script setup lang="ts">
import { onMounted, ref } from 'vue'

defineProps<{ childName: string; motherName: string }>()

interface Petal {
  id: number
  left: number
  delay: number
  duration: number
  size: number
  color: string
}

const PETAL_COLORS = ['#C9A0A8', '#DEB8BC', '#B89090', '#E8D0D0', '#C4B0B4']
const petals = ref<Petal[]>([])

onMounted(() => {
  petals.value = Array.from({ length: 20 }, (_, i) => ({
    id: i,
    left:     Math.random() * 100,
    delay:    Math.random() * 12,
    duration: 9 + Math.random() * 8,
    size:     10 + Math.random() * 18,
    color:    PETAL_COLORS[Math.floor(Math.random() * PETAL_COLORS.length)],
  }))
})
</script>

<template>
  <section class="hero">
    <div class="petals" aria-hidden="true">
      <span
        v-for="p in petals"
        :key="p.id"
        class="petal"
        :style="{
          left:              p.left + '%',
          animationDelay:    p.delay + 's',
          animationDuration: p.duration + 's',
          width:             p.size + 'px',
          height:            p.size + 'px',
          background:        p.color,
        }"
      />
    </div>

    <div class="content">
      <svg class="ornament" viewBox="0 0 340 28" aria-hidden="true">
        <line x1="0"   y1="14" x2="128" y2="14" stroke="var(--rose-deep)" stroke-width="0.6" opacity="0.7"/>
        <path d="M138,14 Q146,6 154,14 Q162,22 170,14 Q178,6 186,14 Q194,22 202,14" fill="none" stroke="var(--rose-deep)" stroke-width="0.6" opacity="0.7"/>
        <line x1="212" y1="14" x2="340" y2="14" stroke="var(--rose-deep)" stroke-width="0.6" opacity="0.7"/>
      </svg>

      <p class="eyebrow">pour toi,</p>

      <h1>
        Bonne<br />
        <em>Fête des Mères</em>
      </h1>

      <p class="dedication">{{ motherName }}</p>

      <svg class="rosette" viewBox="0 0 60 60" aria-hidden="true">
        <g transform="translate(30,30)">
          <ellipse rx="16" ry="6" fill="var(--rose)" opacity="0.35" transform="rotate(0)"/>
          <ellipse rx="16" ry="6" fill="var(--rose)" opacity="0.35" transform="rotate(45)"/>
          <ellipse rx="16" ry="6" fill="var(--rose)" opacity="0.35" transform="rotate(90)"/>
          <ellipse rx="16" ry="6" fill="var(--rose)" opacity="0.35" transform="rotate(135)"/>
          <circle r="5" fill="var(--rose-deep)" opacity="0.5"/>
        </g>
      </svg>

      <p class="signature-line">
        avec tout mon amour,<br />
        <span class="child-name">{{ childName }}</span>
      </p>
    </div>

    <div class="scroll-hint" aria-hidden="true">
      <div class="scroll-bar" />
    </div>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  min-height: 100svh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  overflow: hidden;
  background: linear-gradient(155deg, var(--ivory) 0%, var(--cream) 55%, #EAD8D2 100%);
}

.petals {
  position: absolute;
  inset: 0;
  pointer-events: none;
  z-index: 0;
}

.petal {
  position: absolute;
  top: -30px;
  border-radius: 50% 0 50% 0;
  opacity: 0.6;
  animation: fall linear infinite;
}

@keyframes fall {
  0%   { transform: translateY(0)     rotate(0deg)   translateX(0);    opacity: 0;   }
  8%   {                                                                 opacity: 0.6; }
  45%  { transform: translateY(45vh)  rotate(360deg) translateX(35px);              }
  92%  {                                                                 opacity: 0.3; }
  100% { transform: translateY(112vh) rotate(720deg) translateX(-10px); opacity: 0;   }
}

.content {
  position: relative;
  z-index: 1;
  text-align: center;
  padding: 4rem 2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 1.6rem;
}

.ornament { width: 300px; }
.rosette  { width: 54px; height: 54px; }

.eyebrow {
  font-size: 0.8rem;
  letter-spacing: 0.28em;
  text-transform: uppercase;
  color: var(--rose-deep);
  animation: fadeUp 1.2s ease both 0.2s;
}

h1 {
  font-family: var(--font-display);
  font-size: clamp(3.5rem, 10vw, 8rem);
  font-weight: 300;
  line-height: 1.05;
  animation: fadeUp 1.2s ease both 0.4s;
}

h1 em {
  font-style: italic;
  color: var(--burgundy);
}

.dedication {
  font-family: var(--font-display);
  font-size: 1.4rem;
  font-style: italic;
  font-weight: 300;
  color: var(--text-muted);
  animation: fadeUp 1.2s ease both 0.6s;
}

.signature-line {
  font-size: 0.82rem;
  letter-spacing: 0.14em;
  color: var(--text-muted);
  line-height: 2;
  animation: fadeUp 1.2s ease both 1s;
}

.child-name {
  font-family: var(--font-display);
  font-size: 1.9rem;
  font-style: italic;
  font-weight: 400;
  color: var(--burgundy);
  display: block;
  margin-top: 0.2rem;
}

.scroll-hint {
  position: absolute;
  bottom: 2.5rem;
  animation: fadeUp 1.2s ease both 1.6s;
}

.scroll-bar {
  width: 1px;
  height: 60px;
  background: linear-gradient(to bottom, var(--rose-deep), transparent);
  margin: 0 auto;
  animation: scrollPulse 2.2s ease infinite;
}

@keyframes scrollPulse {
  0%, 100% { opacity: 0.25; transform: scaleY(1); }
  50%       { opacity: 1;    transform: scaleY(0.65) translateY(12px); }
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(22px); }
  to   { opacity: 1; transform: translateY(0);    }
}
</style>
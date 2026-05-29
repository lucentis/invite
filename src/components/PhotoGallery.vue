<script setup lang="ts">
import { useReveal } from '../composables/useReveal'
import JuVenise from '../assets/images/ju-venise.jpg'
import OscarGrimace from '../assets/images/oscar-grimace.jpg'
import OscarMaman from '../assets/images/oscar-maman.jpg'
import Nous from '../assets/images/nous.jpg'

// Customize captions here

const images = [
  {
    img: Nous,
    caption: 'Mon premier anniversaire'
  },
  {
    img: JuVenise,
    caption: 'Quand tu me portes pour jouer'
  },
  
  {
    img: OscarGrimace,
    caption: 'Quand je fais le foufou'
  },
  {
    img: OscarMaman,
    caption: 'Les meilleurs calîns'
  },
  
]

const { el, visible } = useReveal()
console.log(el);

</script>

<template>
  <section class="gallery" ref="el" :class="{ visible }">
    <header class="section-header">
      <div class="rule" />
      <h2>Nos plus beaux moments</h2>
      <div class="rule" />
    </header>

    <div class="grid">
      <!--
        Pour ajouter vos photos, remplacez le bloc <div class="placeholder"> par :
        <img src="./assets/photo1.jpg" alt="caption" />
        Placez vos fichiers dans src/assets/
      -->
      <article v-for="(image, i) in images" :key="i" :class="`item-${i + 1}`">
        <div class="photo-frame">
          <!-- Remplacer par <img src="..." :alt="caption" /> -->
          <img :src="image.img">
        </div>
        <p class="caption">{{ image.caption }}</p>
      </article>
    </div>
  </section>
</template>

<style scoped>
.gallery {
  padding: 7rem 2rem;
  max-width: 1080px;
  margin: 0 auto;
  opacity: 0;
  transform: translateY(32px);
  transition: opacity 0.9s ease, transform 0.9s ease;
}

.gallery.visible {
  opacity: 1;
  transform: translateY(0);
}

.section-header {
  display: flex;
  align-items: center;
  gap: 1.8rem;
  margin-bottom: 4rem;
}

.rule {
  flex: 1;
  height: 1px;
  background: linear-gradient(to right, transparent, var(--rose), transparent);
}

h2 {
  font-family: var(--font-display);
  font-size: clamp(1.5rem, 4vw, 2.2rem);
  font-weight: 300;
  font-style: italic;
  color: var(--text);
  white-space: nowrap;
}

/* Asymmetric 3-column grid */
.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-auto-rows: 260px;
  gap: 2.2rem;
}

.item-1 { grid-column: 1 / 3; grid-row: 1; }
.item-2 { grid-column: 3;     grid-row: 1 / 3; }
.item-3 { grid-column: 1;     grid-row: 2; }
.item-4 { grid-column: 2;     grid-row: 2; }

@media (max-width: 700px) {
  .grid { grid-template-columns: 1fr; grid-auto-rows: 220px; }
  .item-1, .item-2, .item-3, .item-4 { grid-column: 1; grid-row: auto; }
}

.photo-frame {
  height: 100%;
  overflow: hidden;
  background: var(--cream);
  border: 1px solid rgba(180, 140, 140, 0.2);
}

.photo-frame img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.7s ease;
}

@media (min-width: 701px) {
  .item-1 .photo-frame img {
    object-position: center 40%;
  }
}

@media (max-width: 701px) {
  .item-2 .photo-frame img {
    object-position: center 30%;
  }
}

.photo-frame:hover img { transform: scale(1.04); }

.placeholder {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.8rem;
  color: var(--rose);
  opacity: 0.45;
}

.placeholder svg  { width: 40px; height: 40px; }

.placeholder span {
  font-size: 0.68rem;
  letter-spacing: 0.22em;
  text-transform: uppercase;
}

.caption {
  font-family: var(--font-display);
  font-size: 0.92rem;
  font-style: italic;
  color: var(--text-muted);
  margin-top: 0.65rem;
  padding-left: 0.2rem;
}
</style>
<script setup lang="ts">
import HeroSection    from './components/HeroSection.vue'
import PhotoGallery   from './components/PhotoGallery.vue'
import MessageSection from './components/MessageSection.vue'

// Personnaliser ici
const childName  = 'Oscar'   // Prénom de votre fils
const motherName = 'Maman'  // Comment il appelle sa mère
</script>

<template>
  <HeroSection    :child-name="childName" :mother-name="motherName" />
  <PhotoGallery />
  <MessageSection :child-name="childName" :mother-name="motherName" />
</template>
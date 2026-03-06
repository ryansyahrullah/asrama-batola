<script setup>
import { siteData } from '../constants/siteData'
</script>

<template>
  <section id="lokasi" class="section lokasi-section">
    <h2 class="section-title fade-in-up visible">{{ siteData.lokasi.title }}</h2>

    <div class="map-container glass-card fade-in-up visible">
      <iframe 
        :src="siteData.lokasi.mapSrc"
        width="100%"
        height="100%"
        style="border:0;"
        allowfullscreen=""
        loading="lazy"
        referrerpolicy="no-referrer-when-downgrade">
      </iframe>
    </div>
  </section>
</template>

<style scoped>
.map-container {
  width: 100%;
  height: 450px;
  border-radius: var(--border-radius);
  overflow: hidden;
  box-shadow: var(--shadow-md);
  padding: 0;
  border: 4px solid var(--white);
}

.map-container iframe {
  width: 100%;
  height: 100%;
  display: block;
}

@media (max-width: 768px) {
  .map-container {
    height: 300px;
  }
}
</style>

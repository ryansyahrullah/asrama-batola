<script setup>
import { onMounted } from 'vue'
import AppNavbar from './components/AppNavbar.vue'
import HeroSection from './components/HeroSection.vue'
import FasilitasSection from './components/FasilitasSection.vue'
import GaleriSection from './components/GaleriSection.vue'
import PengurusSection from './components/PengurusSection.vue'
import AturanSection from './components/AturanSection.vue'
import LokasiSection from './components/LokasiSection.vue'
import KontakSection from './components/KontakSection.vue'
import AppFooter from './components/AppFooter.vue'

// Intersection Observer for fade-in animations
onMounted(() => {
  const observer = new IntersectionObserver((entries) => {
    entries.forEach(entry => {
      if (entry.isIntersecting) {
        entry.target.classList.add('visible')
      }
    })
  }, {
    threshold: 0.1,
    rootMargin: "0px 0px -50px 0px"
  })

  // Select all elements with fade-in-up class that aren't already visible (except those deliberately made visible initially)
  document.querySelectorAll('.fade-in-up:not(.visible)').forEach(el => {
    observer.observe(el)
  })
})
</script>

<template>
  <div class="app-container">
    <AppNavbar />
    
    <main>
      <HeroSection />
      <FasilitasSection />
      <GaleriSection />
      <PengurusSection />
      <AturanSection />
      <LokasiSection />
      <KontakSection />
    </main>

    <AppFooter />
  </div>
</template>

<style>
/* Remove visible class from elements that should animate on scroll, 
   except in Hero section where they should be visible immediately */
#fasilitas .fade-in-up,
#galeri .fade-in-up,
#pengurus .fade-in-up,
#aturan .fade-in-up,
#lokasi .fade-in-up,
#kontak .fade-in-up {
  opacity: 0;
  transform: translateY(30px);
}

#fasilitas .fade-in-up.visible,
#galeri .fade-in-up.visible,
#pengurus .fade-in-up.visible,
#aturan .fade-in-up.visible,
#lokasi .fade-in-up.visible,
#kontak .fade-in-up.visible {
  opacity: 1;
  transform: translateY(0);
}
</style>

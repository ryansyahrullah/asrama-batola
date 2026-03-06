<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { siteData } from '../constants/siteData'

const currentSlide = ref(0)
const totalSlides = siteData.hero.images.length
let slideInterval = null
const isRecruitmentModalOpen = ref(false)

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % totalSlides
}

onMounted(() => {
  slideInterval = setInterval(nextSlide, 5000)
})

onUnmounted(() => {
  if (slideInterval) clearInterval(slideInterval)
})
</script>

<template>
  <section id="beranda" class="hero-section">
    <!-- Slider Backgrounds -->
    <div class="slider-container">
      <div 
        v-for="(img, index) in siteData.hero.images" 
        :key="index"
        :class="['slide', { active: currentSlide === index }]"
        :style="{ backgroundImage: `url(${img})` }"
      ></div>
      <div class="overlay"></div>
    </div>

    <!-- Hero Content -->
    <div class="hero-content">
      <h1 class="fade-in-up">{{ siteData.hero.title }}</h1>
      <p class="fade-in-up delay-1">{{ siteData.hero.subtitle }}</p>
      
      <!-- Changed from a link to a button triggering the modal -->
      <button 
        class="cta-btn fade-in-up delay-2" 
        @click="isRecruitmentModalOpen = true"
      >
        {{ siteData.hero.ctaText }}
      </button>
    </div>

    <!-- Recruitment Modal / Lightbox -->
    <Teleport to="body">
      <div 
        v-if="isRecruitmentModalOpen" 
        class="recruitment-modal" 
        @click="isRecruitmentModalOpen = false"
      >
        <div class="modal-content" @click.stop>
          <button class="close-btn" @click="isRecruitmentModalOpen = false">&times;</button>
          <img :src="siteData.hero.rekrutmenImage" alt="Open Recruitment Asrama" class="recruitment-img" />
        </div>
      </div>
    </Teleport>
  </section>
</template>

<style scoped>
.hero-section {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
  background: var(--primary-color-dark);
}

.slider-container {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}

.slider-container .slide {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  transition: opacity 1.5s ease-in-out, transform 8s alternate linear;
  transform: scale(1.05);
  background-size: cover;
  background-position: center;
}

.slider-container .slide.active {
  opacity: 1;
  transform: scale(1);
}

.overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to bottom, rgba(0, 74, 173, 0.4), rgba(0, 0, 0, 0.7));
}

.hero-content {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  text-align: center;
  color: var(--white);
  width: 90%;
  max-width: 800px;
  z-index: 10;
}

.hero-content h1 {
  font-size: 56px;
  line-height: 1.2;
  margin-bottom: 20px;
  font-weight: 800;
  text-shadow: 0 4px 20px rgba(0,0,0,0.5);
}

.hero-content p {
  font-size: 20px;
  margin-bottom: 35px;
  font-weight: 400;
  opacity: 0.9;
  text-shadow: 0 2px 10px rgba(0,0,0,0.5);
}

.cta-btn {
  background: var(--accent-color);
  color: var(--white);
  padding: 15px 30px;
  border-radius: 50px;
  text-decoration: none;
  font-weight: 600;
  font-size: 18px;
  transition: all 0.3s ease;
  border: none;
  cursor: pointer;
}

.cta-btn:hover {
  background: var(--accent-color-dark);
  transform: translateY(-3px);
  box-shadow: 0 10px 20px rgba(0,0,0,0.2);
}

/* Fade-in-up animations */
.fade-in-up {
  opacity: 0;
  transform: translateY(20px);
  transition: opacity 0.6s ease-out, transform 0.6s ease-out;
}

.fade-in-up.visible {
  opacity: 1;
  transform: translateY(0);
}

.fade-in-up.delay-1 { transition-delay: 0.2s; }
.fade-in-up.delay-2 { transition-delay: 0.4s; }

/* Recruitment Modal Styles */
.recruitment-modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: rgba(0, 0, 0, 0.85); /* Dark overlay */
  backdrop-filter: blur(8px);
  z-index: 9999;
  display: flex;
  align-items: center;
  justify-content: center;
  animation: fadeIn 0.3s ease;
  padding: 20px;
}

.modal-content {
  position: relative;
  max-width: 90vw;
  max-height: 90vh;
  background: var(--white);
  border-radius: 12px;
  overflow: hidden;
  box-shadow: 0 25px 50px -12px rgba(0, 0, 0, 0.5);
  animation: scaleUp 0.3s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.recruitment-img {
  display: block;
  max-width: 100%;
  max-height: 90vh;
  object-fit: contain;
}

.close-btn {
  position: absolute;
  top: 15px;
  right: 15px;
  background: rgba(0, 0, 0, 0.5);
  color: white;
  border: none;
  font-size: 28px;
  width: 40px;
  height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.2s ease;
  z-index: 2;
  line-height: 1;
}

.close-btn:hover {
  background: var(--accent-color);
  transform: scale(1.1);
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes scaleUp {
  from { transform: scale(0.95); opacity: 0; }
  to { transform: scale(1); opacity: 1; }
}

@media (max-width: 768px) {
  .hero-content h1 {
    font-size: 36px;
  }
  .hero-content p {
    font-size: 16px;
  }
  .close-btn {
    top: 10px;
    right: 10px;
    width: 35px;
    height: 35px;
    font-size: 24px;
  }
}
</style>

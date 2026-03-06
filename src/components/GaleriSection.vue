<script setup>
import { siteData } from '../constants/siteData'
import { ref } from 'vue'

const isModalOpen = ref(false)
const selectedImage = ref('')

const openModal = (imgSrc) => {
  selectedImage.value = imgSrc
  isModalOpen.value = true
  document.body.style.overflow = 'hidden' // Prevent bg scrolling
}

const closeModal = () => {
  isModalOpen.value = false
  setTimeout(() => { selectedImage.value = '' }, 300)
  document.body.style.overflow = ''
}
</script>

<template>
  <section id="galeri" class="section gallery-section">
    <h2 class="section-title fade-in-up visible">{{ siteData.galeri.title }}</h2>

    <div class="gallery-container">
      <div 
        v-for="(img, index) in siteData.galeri.items" 
        :key="index"
        class="gallery-item glass-card fade-in-up visible"
        :style="`transition-delay: ${index * 0.15}s`"
        @click="openModal(img.src)"
      >
        <img :src="img.src" :alt="img.alt" @error="$event.target.src='https://placehold.co/600x400/004aad/white?text=Gambar+Galeri'" />
        <div class="gallery-overlay">
          <span>{{ img.caption }}</span>
          <div class="zoom-icon">🔍</div>
        </div>
      </div>
    </div>

    <!-- Lightbox Modal -->
    <Teleport to="body">
      <div 
        class="modal-backdrop" 
        :class="{ 'modal-open': isModalOpen }" 
        @click="closeModal"
      >
        <div class="modal-content" @click.stop>
          <button class="close-btn" @click="closeModal">&times;</button>
          <img v-if="selectedImage" :src="selectedImage" alt="Galeri Fullscreen" @error="$event.target.src='https://placehold.co/1200x800/004aad/white?text=Gambar+Galeri'" />
        </div>
      </div>
    </Teleport>
  </section>
</template>

<style scoped>
.gallery-section {
  background: var(--white);
  border-radius: var(--border-radius);
  box-shadow: var(--shadow-sm);
}

.gallery-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 25px;
  padding: 10px;
}

.gallery-item {
  position: relative;
  width: 100%;
  aspect-ratio: 4 / 3;
  overflow: hidden;
  cursor: pointer;
  border-radius: var(--border-radius);
}

.gallery-item img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  transition: transform 0.6s cubic-bezier(0.25, 1, 0.5, 1);
}

.gallery-item:hover img {
  transform: scale(1.1);
}

.gallery-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(to top, rgba(0, 51, 127, 0.9) 0%, rgba(0, 74, 173, 0.4) 50%, transparent 100%);
  color: white;
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: flex-end;
  opacity: 0;
  transition: opacity 0.4s ease;
}

.gallery-item:hover .gallery-overlay {
  opacity: 1;
}

.gallery-overlay span {
  font-weight: 600;
  font-size: 18px;
  transform: translateY(20px);
  transition: transform 0.4s ease;
}

.gallery-item:hover .gallery-overlay span {
  transform: translateY(0);
}

.zoom-icon {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%) scale(0.5);
  font-size: 30px;
  opacity: 0;
  transition: all 0.4s cubic-bezier(0.175, 0.885, 0.32, 1.275);
}

.gallery-item:hover .zoom-icon {
  opacity: 1;
  transform: translate(-50%, -50%) scale(1);
}

/* Modal Styling */
.modal-backdrop {
  position: fixed;
  inset: 0;
  background-color: rgba(0, 0, 0, 0.9);
  z-index: 2000;
  display: flex;
  justify-content: center;
  align-items: center;
  opacity: 0;
  pointer-events: none;
  transition: opacity 0.3s ease;
  backdrop-filter: blur(5px);
}

.modal-backdrop.modal-open {
  opacity: 1;
  pointer-events: auto;
}

.modal-content {
  position: relative;
  max-width: 90vw;
  max-height: 90vh;
  transform: scale(0.95);
  transition: transform 0.3s ease;
}

.modal-backdrop.modal-open .modal-content {
  transform: scale(1);
}

.modal-content img {
  max-width: 100%;
  max-height: 90vh;
  object-fit: contain;
  border-radius: 8px;
  box-shadow: 0 10px 30px rgba(0,0,0,0.5);
}

.close-btn {
  position: absolute;
  top: -40px;
  right: -0px;
  background: transparent;
  border: none;
  color: white;
  font-size: 40px;
  cursor: pointer;
  line-height: 1;
  transition: color 0.2s;
}

.close-btn:hover {
  color: var(--accent-color);
}

@media (max-width: 768px) {
  .close-btn {
    top: 10px;
    right: 15px;
    background: rgba(0,0,0,0.5);
    width: 40px;
    height: 40px;
    border-radius: 50%;
    font-size: 24px;
    display: flex;
    justify-content: center;
    align-items: center;
  }
}
</style>

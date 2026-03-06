<script setup>
import { siteData } from '../constants/siteData'
</script>

<template>
  <section id="fasilitas" class="section">
    <h2 class="section-title fade-in-up visible">{{ siteData.fasilitas.title }}</h2>

    <div class="card-container">
      <div 
        v-for="(item, index) in siteData.fasilitas.items" 
        :key="index"
        class="card glass-card fade-in-up visible"
        :style="`transition-delay: ${index * 0.15}s`"
      >
        <div class="icon">{{ item.icon }}</div>
        <h3>{{ item.title }}</h3>
        <p>{{ item.desc }}</p>
      </div>
    </div>
  </section>
</template>

<style scoped>
.card-container {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
  gap: 30px;
  margin-top: 50px;
}

.card {
  padding: 40px 30px;
  text-align: center;
  position: relative;
  overflow: hidden;
  z-index: 1;
}

.card::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: linear-gradient(135deg, rgba(255,255,255,0.4) 0%, rgba(255,255,255,0) 100%);
  z-index: -1;
}

.icon {
  font-size: 50px;
  margin-bottom: 20px;
  display: inline-block;
  background: var(--bg-light);
  width: 90px;
  height: 90px;
  line-height: 90px;
  border-radius: 50%;
  box-shadow: 0 4px 10px rgba(0,0,0,0.05);
  transition: var(--transition);
}

.card:hover .icon {
  transform: scale(1.1) rotate(5deg);
  box-shadow: 0 8px 20px rgba(0,0,0,0.1);
}

.card h3 {
  font-size: 22px;
  color: var(--primary-color-dark);
  margin-bottom: 15px;
  font-weight: 700;
}

.card p {
  color: var(--text-light);
  font-size: 15px;
  line-height: 1.6;
}
</style>

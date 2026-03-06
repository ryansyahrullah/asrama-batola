<script setup>
import { siteData } from '../constants/siteData'
</script>

<template>
  <section id="kontak" class="section kontak-section">
    <h2 class="section-title fade-in-up visible">{{ siteData.kontak.title }}</h2>

    <div class="contact-wrapper">
      <div class="contact-card glass-card fade-in-up visible">
        <div class="contact-icon">📍</div>
        <div class="contact-info">
          <h3>Alamat</h3>
          <p>{{ siteData.kontak.alamat }}</p>
        </div>
      </div>

      <div class="contact-card glass-card fade-in-up visible" style="transition-delay: 0.15s">
        <div class="contact-icon">📞</div>
        <div class="contact-info">
          <h3>Telepon</h3>
          <p v-for="telp in siteData.kontak.telepon" :key="telp">{{ telp }}</p>
        </div>
      </div>

      <div class="contact-card glass-card fade-in-up visible" style="transition-delay: 0.3s">
        <div class="contact-icon">📧</div>
        <div class="contact-info">
          <h3>Email</h3>
          <a :href="`mailto:${siteData.kontak.email}`">{{ siteData.kontak.email }}</a>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.kontak-section {
  text-align: center;
}

.contact-wrapper {
  display: flex;
  justify-content: center;
  gap: 30px;
  flex-wrap: wrap;
}

.contact-card {
  flex: 1;
  min-width: 250px;
  max-width: 350px;
  background: var(--white);
  padding: 40px 20px;
  border-radius: var(--border-radius);
  display: flex;
  flex-direction: column;
  align-items: center;
  transition: var(--transition);
}

.contact-card:hover {
  transform: translateY(-10px);
  box-shadow: var(--shadow-md);
}

.contact-icon {
  font-size: 40px;
  margin-bottom: 20px;
  background: var(--bg-light);
  width: 80px;
  height: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  color: var(--primary-color);
}

.contact-info h3 {
  font-size: 20px;
  color: var(--primary-color-dark);
  margin-bottom: 15px;
}

.contact-info p, .contact-info a {
  font-size: 16px;
  color: var(--text-light);
  margin-bottom: 5px;
  text-decoration: none;
  font-weight: 500;
}

.contact-info a:hover {
  color: var(--primary-color);
  text-decoration: underline;
}

@media (max-width: 768px) {
  .contact-wrapper {
    flex-direction: column;
    align-items: center;
  }
  .contact-card {
    width: 100%;
  }
}
</style>

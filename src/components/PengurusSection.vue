<script setup>
import { siteData } from '../constants/siteData'
</script>

<template>
  <section id="pengurus" class="section pengurus-section">
    <h2 class="section-title fade-in-up visible">{{ siteData.pengurus.title }}</h2>

    <div class="pengurus-container fade-in-up visible">
      <!-- Pengurus Inti -->
      <div class="inti-grid">
        <div 
          v-for="(person, index) in siteData.pengurus.inti" 
          :key="index"
          class="person-card glass-card"
        >
          <div class="avatar-container">
            <img v-if="person.foto" :src="person.foto" :alt="person.nama" class="avatar-img" />
            <div v-else class="avatar-placeholder">{{ person.nama.charAt(0) }}</div>
          </div>
          <h4>{{ person.nama }}</h4>
          <span class="jabatan focus">{{ person.jabatan }}</span>
        </div>
      </div>

      <!-- Divisi / Bidang -->
      <h3 class="divisi-title fade-in-up visible">Koordinator & Divisi</h3>
      <div class="divisi-grid">
        <div 
          v-for="(divisi, index) in siteData.pengurus.divisi" 
          :key="index"
          class="divisi-card glass-card fade-in-up visible"
          :style="`transition-delay: ${index * 0.1}s`"
        >
          <div class="divisi-header">
            <h4>Bidang {{ divisi.nama }}</h4>
          </div>
          <div class="divisi-body">
            <div class="co-person">
              <span class="role">CO (Koordinator)</span>
              <strong>{{ divisi.co }}</strong>
            </div>
            <div class="anggota-list" v-if="divisi.anggota.length > 0">
              <span class="role">Anggota:</span>
              <ul>
                <li v-for="(anggota, idx) in divisi.anggota" :key="idx">{{ anggota }}</li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.pengurus-section {
  text-align: center;
}

.inti-grid {
  display: flex;
  justify-content: center;
  flex-wrap: wrap;
  gap: 25px;
  margin-bottom: 60px;
}

.person-card {
  width: 200px;
  padding: 30px 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: var(--white);
  border-top: 4px solid var(--accent-color);
}

.avatar-container {
  width: 90px;
  height: 90px;
  border-radius: 50%;
  margin-bottom: 15px;
  box-shadow: var(--shadow-sm);
  border: 3px solid var(--white);
  overflow: hidden;
  background: var(--bg-light);
  display: flex;
  align-items: center;
  justify-content: center;
}

.avatar-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  object-position: top; /* Focus on face usually at top of portrait */
}

.avatar-placeholder {
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 32px;
  font-weight: 700;
  color: var(--primary-color);
}

.person-card h4 {
  font-size: 16px;
  color: var(--text-dark);
  margin-bottom: 5px;
}

.jabatan {
  font-size: 13px;
  color: var(--white);
  background: var(--primary-color-dark);
  padding: 4px 12px;
  border-radius: 20px;
  font-weight: 600;
}

.jabatan.focus {
  background: var(--primary-color);
}

.divisi-title {
  font-size: 26px;
  color: var(--primary-color-dark);
  margin-bottom: 30px;
  text-align: center;
}

.divisi-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 25px;
}

.divisi-card {
  background: var(--white);
  overflow: hidden;
  text-align: left;
  display: flex;
  flex-direction: column;
}

.divisi-header {
  background: var(--primary-color);
  color: white;
  padding: 15px 20px;
}

.divisi-header h4 {
  font-size: 16px;
  font-weight: 600;
  letter-spacing: 0.5px;
}

.divisi-body {
  padding: 20px;
  flex-grow: 1;
}

.role {
  font-size: 12px;
  color: var(--text-light);
  text-transform: uppercase;
  letter-spacing: 1px;
  display: block;
  margin-bottom: 4px;
}

.co-person {
  margin-bottom: 15px;
  padding-bottom: 15px;
  border-bottom: 1px dashed rgba(0,0,0,0.1);
}

.co-person strong {
  font-size: 16px;
  color: var(--primary-color-dark);
}

.anggota-list ul {
  list-style: none;
  margin-top: 5px;
}

.anggota-list li {
  font-size: 14px;
  color: var(--text-dark);
  padding: 4px 0 4px 20px;
  position: relative;
}

.anggota-list li::before {
  content: '•';
  color: var(--accent-color);
  position: absolute;
  left: 5px;
  top: 4px;
  font-size: 18px;
}

@media (max-width: 768px) {
  .inti-grid { gap: 10px; margin-bottom: 40px; }
  .person-card { 
    width: calc(50% - 10px); 
    padding: 15px 10px; 
    border-top: 3px solid var(--accent-color);
  }
  .avatar-container { width: 60px; height: 60px; margin-bottom: 10px; }
  .avatar-placeholder { font-size: 20px; }
  .person-card h4 { font-size: 14px; text-align: center; }
  .jabatan { font-size: 11px; padding: 3px 8px; }
  
  .divisi-title { font-size: 22px; margin-bottom: 20px; }
  .divisi-grid { grid-template-columns: 1fr; gap: 15px; }
}
</style>

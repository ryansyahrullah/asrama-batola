<script setup>
const handleImageError = (event) => {
  const target = event.target
  if (target) {
    target.src = 'https://placehold.co/100x100/004aad/white?text=Asrama'
  }
}
</script>

<template>
  <footer class="app-footer">
    <div class="footer-content">
      <div class="footer-logo">
        <img src="../assets/images/logo_asrama.jpg" alt="Logo Asrama Putra" class="footer-img" @error="handleImageError" />
        <h3>Asrama Putra Handil Bakti</h3>
        <p>Tempat tinggal yang aman, nyaman, dan mendukung aktivitas belajar Anda.</p>
      </div>

      <div class="footer-links">
        <h4>Link Cepat</h4>
        <ul>
          <li><a href="#beranda">Beranda</a></li>
          <li><a href="#fasilitas">Fasilitas</a></li>
          <li><a href="#galeri">Galeri</a></li>
          <li><a href="#pengurus">Pengurus</a></li>
          <li><a href="#aturan">Aturan</a></li>
        </ul>
      </div>

      <div class="footer-social">
        <h4>Ikuti Kami</h4>
        <div class="social-links">
          <a href="https://www.instagram.com/asrama_putrabatola/" target="_blank" rel="noopener noreferrer" class="social-link" aria-label="Instagram Asrama Putra">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
              <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
              <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
            </svg>
            <span>@asrama_putrabatola</span>
          </a>
          <a href="https://www.instagram.com/asrama_putribatola/" target="_blank" rel="noopener noreferrer" class="social-link" aria-label="Instagram Asrama Putri">
            <svg xmlns="http://www.w3.org/2000/svg" width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round">
              <rect x="2" y="2" width="20" height="20" rx="5" ry="5"></rect>
              <path d="M16 11.37A4 4 0 1 1 12.63 8 4 4 0 0 1 16 11.37z"></path>
              <line x1="17.5" y1="6.5" x2="17.51" y2="6.5"></line>
            </svg>
            <span>@asrama_putribatola</span>
          </a>
        </div>
      </div>
    </div>
    
    <div class="footer-bottom">
      <p>&copy; {{ new Date().getFullYear() }} Asrama Putra Handil Bakti | Website Resmi</p>
    </div>
  </footer>
</template>

<style scoped>
.app-footer {
  background: linear-gradient(135deg, var(--primary-color-dark) 0%, var(--primary-color) 100%);
  color: var(--white);
  padding: 60px 5% 0;
  margin-top: 50px;
}

.footer-content {
  display: grid;
  grid-template-columns: 2fr 1fr 1fr;
  gap: 40px;
  max-width: 1200px;
  margin: 0 auto;
  padding-bottom: 40px;
  border-bottom: 1px solid rgba(255,255,255,0.1);
}

.footer-logo {
  max-width: 350px;
}

.footer-img {
  width: 60px;
  height: 60px;
  border-radius: 50%;
  margin-bottom: 15px;
  border: 2px solid white;
}

.footer-logo h3 {
  font-size: 22px;
  margin-bottom: 15px;
  font-weight: 700;
}

.footer-logo p {
  color: rgba(255,255,255,0.8);
  font-size: 15px;
  line-height: 1.6;
}

.footer-links h4, .footer-social h4 {
  font-size: 18px;
  margin-bottom: 25px;
  font-weight: 600;
  position: relative;
  display: inline-block;
}

.footer-links h4::after, .footer-social h4::after {
  content: '';
  position: absolute;
  left: 0;
  bottom: -8px;
  width: 30px;
  height: 2px;
  background: var(--accent-color);
}

.footer-links ul {
  list-style: none;
}

.footer-links li {
  margin-bottom: 12px;
}

.footer-links a {
  color: rgba(255,255,255,0.8);
  text-decoration: none;
  font-size: 15px;
  transition: var(--transition);
}

.footer-links a:hover {
  color: var(--accent-color);
  padding-left: 5px;
}

.social-links {
  display: flex;
  flex-direction: column;
  gap: 15px;
}

.social-link {
  display: inline-flex;
  align-items: center;
  gap: 10px;
  color: rgba(255,255,255,0.8);
  text-decoration: none;
  font-weight: 500;
  font-size: 15px;
  transition: var(--transition);
  padding: 8px 15px;
  background: rgba(255,255,255,0.05);
  border-radius: 30px;
  border: 1px solid rgba(255,255,255,0.1);
  width: fit-content;
}

.social-link svg {
  color: var(--white);
  transition: var(--transition);
}

.social-link:hover {
  background: rgba(255,255,255,0.1);
  color: var(--white);
  transform: translateY(-2px);
  border-color: rgba(255,255,255,0.3);
}

.social-link:hover svg {
  color: var(--accent-color);
}

.footer-bottom {
  text-align: center;
  padding: 25px 0;
  font-size: 14px;
  color: rgba(255,255,255,0.7);
}

@media (max-width: 768px) {
  .footer-content {
    grid-template-columns: 1fr;
    text-align: center;
  }
  
  .footer-logo h3::after, .footer-links h4::after, .footer-social h4::after {
    left: 50%;
    transform: translateX(-50%);
  }
  
  .footer-logo {
    margin: 0 auto;
  }
  
  .social-links {
    align-items: center;
  }
}
</style>

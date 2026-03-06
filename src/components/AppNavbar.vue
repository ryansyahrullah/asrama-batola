<script setup>
import { onMounted, onUnmounted, ref } from 'vue'

const isScrolled = ref(false)
const isMobileMenuOpen = ref(false)
const isDropdownOpen = ref(false)

const handleScroll = () => {
  isScrolled.value = window.scrollY > 50
  if (isDropdownOpen.value) {
    isDropdownOpen.value = false
  }
}

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}

const closeMobileMenu = () => {
  isMobileMenuOpen.value = false
  isDropdownOpen.value = false
}

const toggleDropdown = (e) => {
  if (e) e.preventDefault()
  isDropdownOpen.value = !isDropdownOpen.value
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <header :class="['navbar', { 'navbar-scrolled': isScrolled }]">
    <div class="logo-box">
      <img src="../assets/images/logo_asrama.jpg" class="logo-img" alt="Logo Asrama" @error="$event.target.src='https://placehold.co/100x100/004aad/white?text=Asrama'" />
      <span class="logo-text">Asrama Putra Handil Bakti</span>
    </div>

    <button class="hamburger" @click="toggleMobileMenu" aria-label="Menu">
      <span :class="['bar', { 'bar-open-1': isMobileMenuOpen }]"></span>
      <span :class="['bar', { 'bar-open-2': isMobileMenuOpen }]"></span>
      <span :class="['bar', { 'bar-open-3': isMobileMenuOpen }]"></span>
    </button>

    <nav :class="['nav-links', { 'nav-open': isMobileMenuOpen }]">
      <a href="#beranda" @click="closeMobileMenu">Beranda</a>
      <a href="#galeri" @click="closeMobileMenu">Galeri</a>
      
      <!-- Dropdown Menu -->
      <div :class="['dropdown', { 'dropdown-active': isDropdownOpen }]" @mouseenter="isDropdownOpen = true" @mouseleave="isDropdownOpen = false">
        <a href="#" class="dropdown-toggle" @click.prevent="toggleDropdown">
          Tentang <span class="caret">▼</span>
        </a>
        <div class="dropdown-menu">
          <a href="#pengurus" @click="closeMobileMenu">Pengurus</a>
          <a href="#fasilitas" @click="closeMobileMenu">Fasilitas</a>
          <a href="#aturan" @click="closeMobileMenu">Aturan</a>
        </div>
      </div>
      
      <a href="#lokasi" @click="closeMobileMenu">Lokasi</a>
      <a href="#kontak" @click="closeMobileMenu">Kontak</a>
    </nav>
  </header>
</template>

<style scoped>
.navbar {
  width: 100%;
  background: transparent;
  color: var(--white);
  padding: 25px 5%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: fixed;
  top: 0;
  z-index: 1000;
  transition: var(--transition);
}

.navbar-scrolled {
  background: var(--glass-bg);
  backdrop-filter: blur(15px);
  -webkit-backdrop-filter: blur(15px);
  padding: 15px 5%;
  box-shadow: var(--shadow-md);
  color: var(--primary-color-dark);
}

.logo-box {
  display: flex;
  align-items: center;
  gap: 15px;
}

.logo-img {
  width: 45px;
  height: 45px;
  border-radius: 50%;
  object-fit: cover;
  box-shadow: 0 2px 10px rgba(0,0,0,0.1);
}

.logo-text {
  font-size: 20px;
  font-weight: 700;
  letter-spacing: 0.5px;
}

.navbar hr { display: none; }

.nav-links {
  display: flex;
  gap: 30px;
}

.nav-links a {
  text-decoration: none;
  color: inherit;
  font-size: 16px;
  font-weight: 600;
  position: relative;
  transition: var(--transition);
}

.nav-links a:hover {
  color: var(--accent-color);
}

.nav-links a::after {
  content: "";
  position: absolute;
  width: 0%;
  height: 3px;
  bottom: -6px;
  left: 0;
  background: var(--accent-color);
  transition: var(--transition);
  border-radius: 2px;
}

.nav-links a:hover::after {
  width: 100%;
}

/* Dropdown CSS */
.dropdown {
  position: relative;
  display: flex;
  align-items: center;
}

.dropdown-toggle {
  display: flex;
  align-items: center;
  gap: 5px;
}

.caret {
  font-size: 10px;
  transition: transform 0.3s ease;
}

.dropdown:hover .caret,
.dropdown-active .caret {
  transform: rotate(180deg);
}

.dropdown-menu {
  position: absolute;
  top: 100%;
  left: 50%;
  transform: translateX(-50%) translateY(15px);
  background: var(--white);
  min-width: 180px;
  border-radius: 8px;
  box-shadow: var(--shadow-md);
  padding: 10px 0;
  opacity: 0;
  visibility: hidden;
  transition: all 0.3s ease;
  z-index: 1002;
}

/* Show Dropdown on hover (desktop) or active state (mobile/click) */
.dropdown:hover .dropdown-menu,
.dropdown-active .dropdown-menu {
  opacity: 1;
  visibility: visible;
  transform: translateX(-50%) translateY(5px);
}

.dropdown-menu a {
  display: block;
  padding: 10px 20px;
  color: var(--text-dark);
  font-weight: 500;
  transition: background 0.2s, color 0.2s;
}

.dropdown-menu a::after {
  display: none; /* Hide hover underline in dropdown */
}

.dropdown-menu a:hover {
  background: var(--bg-light);
  color: var(--primary-color);
}

.hamburger {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
  flex-direction: column;
  gap: 6px;
  z-index: 1001;
}

.bar {
  width: 30px;
  height: 3px;
  background-color: currentColor;
  border-radius: 3px;
  transition: var(--transition);
}

@media (max-width: 900px) {
  .hamburger {
    display: flex;
  }
  
  .nav-links {
    position: absolute;
    top: 100%;
    left: 0;
    width: 100%;
    background: var(--white);
    flex-direction: column;
    align-items: center;
    padding: 0;
    max-height: 0;
    overflow: hidden;
    color: var(--primary-color-dark);
    box-shadow: var(--shadow-md);
    transition: max-height 0.4s ease;
  }
  
  .nav-open {
    padding: 20px 0;
    max-height: 500px; /* Increased for dropdown */
    overflow-y: auto;
  }
  
  /* Mobile Dropdown Adjustments */
  .dropdown {
    width: 100%;
    flex-direction: column;
    align-items: center;
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }
  
  .dropdown-toggle {
    width: 100%;
    justify-content: center;
    padding: 15px 0;
  }

  .dropdown-menu {
    position: static;
    transform: none;
    box-shadow: none;
    background: rgba(255, 255, 255, 0.05); /* Slight tint for contrast */
    opacity: 1;
    visibility: visible;
    display: none;
    width: 100%;
    padding: 0;
    border-radius: 0;
  }
  
  .dropdown-active .dropdown-menu,
  .dropdown:hover .dropdown-menu {
    display: flex;
    flex-direction: column;
    transform: none;
  }

  .dropdown-menu a {
    text-align: center;
    padding: 12px 0;
    font-size: 14px;
    color: var(--primary-color-dark);
    border-bottom: 1px solid rgba(0, 0, 0, 0.05);
  }
  
  .dropdown-menu a:last-child {
    border-bottom: none;
  }
  
  .dropdown-menu a:hover {
    background: rgba(0, 0, 0, 0.05);
    color: var(--accent-color);
  }
  
  .bar-open-1 { transform: translateY(9px) rotate(45deg); }
  .bar-open-2 { opacity: 0; }
  .bar-open-3 { transform: translateY(-9px) rotate(-45deg); }
}
</style>

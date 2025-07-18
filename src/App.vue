<script setup lang="ts">
import { reactive, computed } from 'vue'

// Brands 3D slider logic
const brands = [
  { name: 'Brand 1', img: '/src/assets/brand1.png' },
  { name: 'Brand 2', img: '/src/assets/brand2.png' },
  { name: 'Brand 3', img: '/src/assets/brand3.png' },
  { name: 'Brand 4', img: '/src/assets/brand4.png' },
  { name: 'Brand 5', img: '/src/assets/brand5.png' },
]

const brandsState = reactive({ angle: 0 })
const totalBrands = brands.length
const radius = 600 // px, distance from center

// Automatic rotation for brands slider
import { onMounted as onMountedBrands, onUnmounted as onUnmountedBrands } from 'vue'
let brandsInterval: number | undefined
onMountedBrands(() => {
  brandsInterval = window.setInterval(() => {
    brandsState.angle += 360 / totalBrands / 80 // smooth step
  }, 80) // 80 steps per brand, 1s per brand
})
onUnmountedBrands(() => {
  if (brandsInterval) clearInterval(brandsInterval)
})

function getBrandSlideStyle(idx: number) {
  const angle = (360 / totalBrands) * idx - brandsState.angle
  return {
    transform: `rotateY(${angle}deg) translateZ(${radius}px)`,
  }
}

const brandsSliderStyle = computed(() => ({
  transform: `rotateX(5deg) translateZ(-${radius}px)`,
}))
function smoothScrollToElement(element: HTMLElement | null) {
  if (!element) return
  const headerOffset = 100 // height of your fixed header
  const elementPosition = element.getBoundingClientRect().top + window.pageYOffset
  const offsetPosition = elementPosition - headerOffset
  const start = window.scrollY || window.pageYOffset
  const distance = offsetPosition - start
  const duration = 600
  let startTime: number | null = null

  function animation(currentTime: number) {
    if (startTime === null) startTime = currentTime
    const timeElapsed = currentTime - (startTime as number)
    const run = easeInOutQuad(timeElapsed, start, distance, duration)
    window.scrollTo(0, run)
    if (timeElapsed < duration) requestAnimationFrame(animation)
    else window.scrollTo(0, offsetPosition)
  }

  function easeInOutQuad(t: number, b: number, c: number, d: number): number {
    t /= d / 2
    if (t < 1) return (c / 2) * t * t + b
    t--
    return (-c / 2) * (t * (t - 2) - 1) + b
  }

  requestAnimationFrame(animation)
}

function goHomeAndScrollToContact() {
  if (route.path !== '/') {
    router.push('/').then(() => {
      setTimeout(() => {
        const contactSection = document.getElementById('contact-section')
        if (contactSection) smoothScrollToElement(contactSection)
      }, 300)
    })
  } else {
    const contactSection = document.getElementById('contact-section')
    if (contactSection) smoothScrollToElement(contactSection)
  }
}

function goHomeAndScrollToAbout() {
  if (route.path !== '/') {
    router.push('/').then(() => {
      setTimeout(() => {
        const aboutSection = document.getElementById('about-section')
        if (aboutSection) smoothScrollToElement(aboutSection)
      }, 300)
    })
  } else {
    const aboutSection = document.getElementById('about-section')
    if (aboutSection) smoothScrollToElement(aboutSection)
  }
}
import { RouterLink, useRouter, useRoute } from 'vue-router'
import { ref, onMounted, onUnmounted } from 'vue'

const router = useRouter()
const route = useRoute()
function goHomeAndScrollTop() {
  if (route.path !== '/') {
    router.push('/').then(() => {
      window.scrollTo({ top: 0, behavior: 'smooth' })
    })
  } else {
    window.scrollTo({ top: 0, behavior: 'smooth' })
  }
}

const galleryImages = [
  '/src/assets/cover.png',
  '/src/assets/IMG_6650.png',
  '/src/assets/IMG_6660.png',
]
const currentGalleryIndex = ref(0)
let galleryInterval: number | undefined

onMounted(() => {
  galleryInterval = window.setInterval(() => {
    currentGalleryIndex.value = (currentGalleryIndex.value + 1) % galleryImages.length
  }, 3000)
})
onUnmounted(() => {
  if (galleryInterval) clearInterval(galleryInterval)
})
</script>

<template>
  <header>
    <nav class="navbar">
      <img src="@/assets/Logo14.png" alt="Logo" class="navbar-logo" width="32" height="32" />
      <div class="navbar-tabs">
        <a href="#" class="nav-tab" @click.prevent="goHomeAndScrollTop">Home</a>
        <RouterLink to="/products" class="nav-tab">Products</RouterLink>
        <a href="#contact-section" class="nav-tab" @click.prevent="goHomeAndScrollToContact"
          >Contact Us</a
        >
        <a href="#about-section" class="nav-tab" @click.prevent="goHomeAndScrollToAbout">About</a>
      </div>
    </nav>
  </header>

  <div class="background-gallery-container">
    <div class="gallery-fade">
      <img
        v-for="(img, idx) in galleryImages"
        :key="img"
        :src="img"
        :class="{ active: idx === currentGalleryIndex }"
        class="gallery-img"
      />
    </div>
    <div class="welcome-text">Welcome to Hikari</div>
  </div>

  <div class="products-section" id="products-section">
    <h2 class="products-title">Our Products</h2>
    <div class="products-container">
      <div class="product-card">
        <div class="product-image-container">
          <img src="/src/assets/cover.png" alt="Product 1" class="product-image" />
          <div class="product-title-overlay">Product 1</div>
        </div>
      </div>
      <div class="product-card">
        <div class="product-image-container">
          <img src="/src/assets/IMG_6650.png" alt="Product 2" class="product-image" />
          <div class="product-title-overlay">Product 2</div>
        </div>
      </div>
      <div class="product-card">
        <div class="product-image-container">
          <img src="/src/assets/IMG_6660.png" alt="Product 3" class="product-image" />
          <div class="product-title-overlay">Product 3</div>
        </div>
      </div>
      <div class="product-card">
        <div class="product-image-container">
          <img src="/src/assets/IMG_6614.png" alt="Product 4" class="product-image" />
          <div class="product-title-overlay">Product 4</div>
        </div>
      </div>
      <div class="product-card">
        <div class="product-image-container">
          <img src="/src/assets/IMG_6617.png" alt="Product 5" class="product-image" />
          <div class="product-title-overlay">Product 5</div>
        </div>
      </div>
      <div class="product-card">
        <div class="product-image-container">
          <img src="/src/assets/IMG_6655.png" alt="Product 6" class="product-image" />
          <div class="product-title-overlay">Product 6</div>
        </div>
      </div>
    </div>
  </div>

  <!-- About Section -->
  <section class="about-section" id="about-section">
    <h2 class="about-title">About</h2>
    <div class="about-containers">
      <!-- WHO ARE WE -->
      <div class="about-card who-are-we">
        <div class="about-card-content">
          <div class="about-card-title">WHO ARE WE</div>
          <div class="about-card-text">
            We are Hikari, a company dedicated to providing innovative products and exceptional
            service to our customers.
          </div>
        </div>
      </div>
      <!-- Mission -->
      <div class="about-card mission">
        <div class="about-card-image left">
          <img src="/src/assets/cover.png" alt="Mission" />
        </div>
        <div class="about-card-content">
          <div class="about-card-title">Mission</div>
          <div class="about-card-text">
            Our mission is to illuminate lives through quality products and a commitment to
            excellence.
          </div>
        </div>
      </div>
      <!-- Vision -->
      <div class="about-card vision">
        <div class="about-card-content">
          <div class="about-card-title">Vision</div>
          <div class="about-card-text">
            Our vision is to be a beacon of innovation and trust in the industry, inspiring brighter
            futures for all.
          </div>
        </div>
        <div class="about-card-image right">
          <img src="/src/assets/IMG_6650.png" alt="Vision" />
        </div>
      </div>
    </div>
  </section>

  <!-- Brands We Carry Section -->
  <section class="brands-section" id="brands-section">
    <h2 class="brands-title">Brands We Carry</h2>
    <div class="brands-slider-container">
      <div class="brands-slider-3d" :style="brandsSliderStyle">
        <div
          v-for="(brand, idx) in brands"
          :key="brand.img"
          class="brand-slide"
          :style="getBrandSlideStyle(idx)"
        >
          <div class="brand-slide-front">
            <img :src="brand.img" :alt="brand.name" class="brand-img" />
          </div>
          <div class="brand-slide-back"></div>
        </div>
      </div>
    </div>
  </section>

  <!-- Contact Section -->
  <section class="contact-section" id="contact-section">
    <h2 class="contact-title">Contact</h2>
    <div class="contact-containers">
      <div class="contact-card facebook">
        <div class="contact-icon">
          <svg
            width="40"
            height="40"
            viewBox="0 0 24 24"
            fill="#1877F3"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M22.675 0h-21.35C.595 0 0 .595 0 1.326v21.348C0 23.405.595 24 1.326 24h11.495v-9.294H9.691v-3.622h3.13V8.413c0-3.1 1.893-4.788 4.659-4.788 1.325 0 2.463.099 2.797.143v3.24l-1.918.001c-1.504 0-1.797.715-1.797 1.763v2.313h3.587l-.467 3.622h-3.12V24h6.116C23.405 24 24 23.405 24 22.674V1.326C24 .595 23.405 0 22.675 0z"
            />
          </svg>
        </div>
        <div class="contact-label">Facebook</div>
      </div>
      <div class="contact-card telegram">
        <div class="contact-icon">
          <svg
            width="40"
            height="40"
            viewBox="0 0 24 24"
            fill="#0088cc"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M12 0C5.371 0 0 5.371 0 12c0 6.629 5.371 12 12 12s12-5.371 12-12c0-6.629-5.371-12-12-12zm5.707 7.293l-2.828 10.607c-.213.799-.771.992-1.562.617l-2.156-1.592-1.04 1.001c-.115.115-.211.211-.432.211l.155-2.197 7.995-7.211c.174-.155-.038-.242-.271-.087l-9.885 6.221-2.13-.664c-.776-.242-.792-.776.162-1.147l13.322-5.142c.623-.242 1.174.155.974 1.08z"
            />
          </svg>
        </div>
        <div class="contact-label">Telegram</div>
      </div>
      <div class="contact-card whatsapp">
        <div class="contact-icon">
          <svg
            width="40"
            height="40"
            viewBox="0 0 24 24"
            fill="#25D366"
            xmlns="http://www.w3.org/2000/svg"
          >
            <path
              d="M20.52 3.48A11.93 11.93 0 0012 0C5.373 0 0 5.373 0 12c0 2.11.55 4.16 1.6 5.98L0 24l6.26-1.64A11.94 11.94 0 0012 24c6.627 0 12-5.373 12-12 0-3.19-1.24-6.19-3.48-8.52zM12 22c-1.85 0-3.66-.5-5.22-1.44l-.37-.22-3.72.98.99-3.62-.24-.38A9.94 9.94 0 012 12c0-5.52 4.48-10 10-10s10 4.48 10 10-4.48 10-10 10zm5.2-7.6c-.28-.14-1.65-.81-1.9-.9-.25-.09-.43-.14-.61.14-.18.28-.7.9-.86 1.08-.16.18-.32.2-.6.07-.28-.14-1.18-.44-2.25-1.4-.83-.74-1.39-1.65-1.55-1.93-.16-.28-.02-.43.12-.57.13-.13.28-.34.42-.51.14-.17.18-.29.28-.48.09-.19.05-.36-.02-.5-.07-.14-.61-1.47-.84-2.01-.22-.53-.45-.46-.62-.47-.16-.01-.36-.01-.56-.01-.19 0-.5.07-.76.34-.26.27-1 1-.99 2.43.01 1.43 1.03 2.81 1.18 3 .15.19 2.03 3.1 4.93 4.22.69.3 1.23.48 1.65.61.69.22 1.32.19 1.81.12.55-.08 1.65-.67 1.89-1.32.23-.65.23-1.2.16-1.32-.07-.12-.25-.19-.53-.33z"
            />
          </svg>
        </div>
        <div class="contact-label">WhatsApp</div>
      </div>
    </div>
  </section>
  <section class="footer">
    <div class="footer-main">
      <div class="footer-col footer-col-left">
        <img src="@/assets/Logo14.png" alt="Logo" class="footer-logo" width="40" height="40" />
        <div class="footer-contact">
          <span>Contact us:</span>
          <span>+1 (234) 567-8901</span>
        </div>
      </div>
      <div class="footer-col footer-col-right">
        <nav class="footer-nav-vertical">
          <RouterLink to="/" class="nav-tab">Home</RouterLink>
          <RouterLink to="/products" class="nav-tab">Products</RouterLink>
          <RouterLink to="/contact" class="nav-tab">Contact Us</RouterLink>
          <a href="#about-section" class="nav-tab" @click.prevent="goHomeAndScrollToAbout">About</a>
        </nav>
        <div class="footer-social">
          <a href="#" aria-label="Facebook" class="footer-social-link">
            <svg
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M22.675 0h-21.35C.595 0 0 .595 0 1.326v21.348C0 23.405.595 24 1.326 24h11.495v-9.294H9.691v-3.622h3.13V8.413c0-3.1 1.893-4.788 4.659-4.788 1.325 0 2.463.099 2.797.143v3.24l-1.918.001c-1.504 0-1.797.715-1.797 1.763v2.313h3.587l-.467 3.622h-3.12V24h6.116C23.405 24 24 23.405 24 22.674V1.326C24 .595 23.405 0 22.675 0z"
                fill="#fff"
              />
            </svg>
          </a>
          <a href="#" aria-label="Twitter" class="footer-social-link">
            <svg
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M24 4.557a9.83 9.83 0 01-2.828.775 4.932 4.932 0 002.165-2.724c-.951.564-2.005.974-3.127 1.195a4.916 4.916 0 00-8.38 4.482C7.691 8.095 4.066 6.13 1.64 3.161c-.543.929-.855 2.006-.855 3.163 0 2.18 1.111 4.104 2.797 5.229a4.904 4.904 0 01-2.229-.616c-.054 2.281 1.581 4.415 3.949 4.89a4.936 4.936 0 01-2.224.084c.627 1.956 2.444 3.377 4.6 3.418A9.867 9.867 0 010 21.543a13.94 13.94 0 007.548 2.212c9.058 0 14.009-7.513 14.009-14.009 0-.213-.005-.425-.014-.636A10.025 10.025 0 0024 4.557z"
                fill="#fff"
              />
            </svg>
          </a>
          <a href="#" aria-label="Instagram" class="footer-social-link">
            <svg
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M12 2.163c3.204 0 3.584.012 4.85.07 1.366.062 2.633.334 3.608 1.308.975.974 1.246 2.242 1.308 3.608.058 1.266.07 1.646.07 4.85s-.012 3.584-.07 4.85c-.062 1.366-.334 2.633-1.308 3.608-.974.975-2.242 1.246-3.608 1.308-1.266.058-1.646.07-4.85.07s-3.584-.012-4.85-.07c-1.366-.062-2.633-.334-3.608-1.308-.975-.974-1.246-2.242-1.308-3.608C2.175 15.647 2.163 15.267 2.163 12s.012-3.584.07-4.85c.062-1.366.334-2.633 1.308-3.608.974-.975 2.242-1.246 3.608-1.308C8.416 2.175 8.796 2.163 12 2.163zm0-2.163C8.741 0 8.332.013 7.052.072 5.775.131 4.602.396 3.635 1.363c-.967.967-1.232 2.14-1.291 3.417C2.013 8.332 2 8.741 2 12c0 3.259.013 3.668.072 4.948.059 1.277.324 2.45 1.291 3.417.967.967 2.14 1.232 3.417 1.291C8.332 23.987 8.741 24 12 24s3.668-.013 4.948-.072c1.277-.059 2.45-.324 3.417-1.291.967-.967 1.232-2.14 1.291-3.417.059-1.28.072-1.689.072-4.948 0-3.259-.013-3.668-.072-4.948-.059-1.277-.324-2.45-1.291-3.417-.967-.967-2.14-1.232-3.417-1.291C15.668.013 15.259 0 12 0zm0 5.838A6.162 6.162 0 005.838 12 6.162 6.162 0 0012 18.162 6.162 6.162 0 0018.162 12 6.162 6.162 0 0012 5.838zm0 10.162A4 4 0 118 12a4 4 0 014 4zm6.406-11.845a1.44 1.44 0 11-2.88 0 1.44 1.44 0 012.88 0z"
                fill="#fff"
              />
            </svg>
          </a>
        </div>
      </div>
    </div>
    <div class="footer-credits">
      <span>© 2025 Your Company. All rights reserved.</span>
    </div>
  </section>
</template>

<style scoped>
/* Our Products container styles */
.products-section {
  width: 1400px;
  height: 300px;
  margin: 10px auto 10px auto;
  background: transparent;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0 2rem 0 2rem;
}
.products-section .products-title {
  color: white;
  font-size: 2rem;
  font-weight: bold;
  background-color: gray;
}
/* Background gallery container styles */
.background-gallery-container {
  width: 100%;
  height: 400px;
  margin-top: 100px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  background: #181818; /* fallback background, adjust as needed */
  overflow: hidden;
}
.gallery-fade {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  z-index: 1;
  overflow: hidden;
}
.gallery-img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  opacity: 0;
  transition: opacity 1.2s ease;
  pointer-events: none;
}
.gallery-img.active {
  opacity: 1;
  z-index: 2;
}

.welcome-text {
  color: #fff;
  font-size: 2.5rem;
  font-weight: bold;
  text-align: center;
  z-index: 2;
  width: 100%;
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
}
html,
body {
  width: 100%;
  max-width: 100vw;
  overflow-x: hidden;
}

.footer {
  width: 100vw;
  max-width: 100vw;
  overflow-x: hidden;
}

body {
  scrollbar-width: none; /* Firefox */
}

body::-webkit-scrollbar {
  display: none; /* Chrome, Safari, Opera */
}
header {
  width: 100vw;
  height: 100px;
  position: fixed;
  top: 0;
  left: 0;
  padding: 0.5rem 2rem;
  z-index: 100;
  background: #000;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.03);
}
nav.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  text-align: left;
  margin-left: 0;
}
/* Navbar styles unified for RouterLink and anchor tags */
.navbar-tabs {
  display: flex;
  align-items: center;
}
.navbar-logo {
  margin: 0 2rem 0 1rem;
  height: 82px;
  width: 175px;
  padding: 0px;
  border: 2px solid white;
}
/* Unified navbar tab styles */
.nav-tab {
  margin: 0 1rem;
  text-decoration: none;
  color: #fff;
  font-size: 1rem;
  opacity: 0.85;
  transition:
    opacity 0.2s,
    font-weight 0.2s;
}
.nav-tab:hover,
.nav-tab.active {
  opacity: 1;
  font-weight: bold;
}
.footer {
  width: 100vw;
  position: static;
  left: 0;
  bottom: 0;
  z-index: 0;
}
.footer-main {
  background: #222;
  color: #fff;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 2rem;
  min-height: 135px;
}
.footer-col {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.footer-col-left {
  align-items: flex-start;
  margin-left: 15rem;
}
.footer-col-right {
  align-items: flex-end;
  margin-right: 15rem;
}
.footer-logo {
  margin-bottom: 0.5rem;
  border-radius: 6px;
  border: 2px solid #fff;
  height: 85px;
  width: 200px;
}
.footer-nav-vertical {
  display: flex;
  flex-direction: row;
  gap: 0;
  align-items: center;
  width: 200px;
  justify-content: space-between;
  padding: 0;
  margin: 0;
}
/* Footer nav unified styles */
/* Unified footer nav tab styles */
.footer-nav-vertical .nav-tab {
  color: #fff;
  font-size: 0.65rem;
  text-decoration: none;
  opacity: 0.8;
  padding: 0;
  margin: 0;
  transition:
    opacity 0.2s,
    font-weight 0.2s;
}
.footer-nav-vertical .nav-tab:hover,
.footer-nav-vertical .nav-tab.active {
  opacity: 1;
  font-weight: bold;
}
.footer-col-right {
  align-items: flex-end;
  justify-content: space-between;
}
.footer-social {
  display: flex;
  flex-direction: row;
  gap: 0.5rem;
  margin-bottom: 1rem;
}
.footer-social-link {
  background: transparent;
  color: #fff;
  border-radius: 50%;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1rem;
  text-decoration: none;
  opacity: 0.7;
  transition:
    background 0.2s,
    opacity 0.2s,
    transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.footer-social-link:hover {
  transform: translateY(-8px);
}

.footer-contact {
  display: flex;
  flex-direction: column;
  color: #fff;
  font-size: 0.95rem;
  margin: 0;
  padding: 0;
}
.footer-contact span {
  width: 100%;
  line-height: 1rem;
  margin: 0;
  padding: 0;
}

.footer-credits {
  background: #000;
  color: #fff;
  text-align: center;
  padding: 0.5rem 0;
  font-size: 0.9rem;
}
.products-container {
  display: flex;
  gap: 1.5rem;
  width: 100%;
  justify-content: center;
  margin-top: 1rem;
  overflow: hidden;
}
.product-card {
  width: 200px;
  height: 200px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 0;
}
.product-title {
  color: #fff;
  font-size: 1.1rem;
  font-weight: bold;
  text-align: center;
  margin-bottom: 0.5rem;
  width: 100%;
  letter-spacing: 0.5px;
}
.product-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  border-radius: 8px;
  display: block;
}
.product-image-container {
  position: relative;
  width: 100%;
  height: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}

.product-title-overlay {
  position: absolute;
  left: 0;
  bottom: 0;
  width: 100%;
  padding: 0.5rem 0;
  color: #fff;
  font-size: 1.1rem;
  font-weight: bold;
  text-align: center;
  border-bottom-left-radius: 8px;
  border-bottom-right-radius: 8px;
  z-index: 2;
  letter-spacing: 0.5px;
}
.about-section {
  width: 100%;
  padding: 4rem;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.about-title {
  color: black;
  font-size: 2.5rem;
  font-weight: bold;
  text-align: center;
  margin-bottom: 0.5rem;
  width: 100%;
  letter-spacing: 0.5px;
}
.about-card {
  width: 100%;
  height: 300px;
  overflow: hidden;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.who-are-we {
  text-align: center;
  justify-content: center;
}
.mission {
}
.vision {
}
.about-card-image {
  width: 40%;
  height: 100%;
  overflow: hidden;
}
.about-card-content {
  width: 60%;
}

/* Contact Section Styles */
.contact-section {
  width: 100%;
  padding: 4rem 0 4rem 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: #f7f7f7;
}
.contact-title {
  color: #222;
  font-size: 2.5rem;
  font-weight: bold;
  text-align: center;
  margin-bottom: 2rem;
  width: 100%;
  letter-spacing: 0.5px;
}
.contact-containers {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: stretch;
  gap: 2rem;
  width: 100%;
  max-width: 900px;
}
.contact-card {
  flex: 1 1 0;
  background: #fff;
  border-radius: 16px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.08);
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 2rem 1rem;
  min-width: 180px;
  max-width: 250px;
  transition:
    box-shadow 0.2s,
    transform 0.2s;
}
.contact-card:hover {
  box-shadow: 0 4px 24px rgba(0, 0, 0, 0.16);
  transform: translateY(-6px) scale(1.04);
}
.contact-icon {
  margin-bottom: 1rem;
}
.contact-label {
  font-size: 1.2rem;
  font-weight: bold;
  color: #222;
  text-align: center;
}
.contact-card.facebook .contact-icon svg {
  filter: drop-shadow(0 2px 6px #1877f3aa);
}
.contact-card.telegram .contact-icon svg {
  filter: drop-shadow(0 2px 6px #0088ccaa);
}
.contact-card.whatsapp .contact-icon svg {
  filter: drop-shadow(0 2px 6px #25d366aa);
}
/* Brands We Carry Section Styles */
.brands-section {
  width: 100%;
  padding: 4rem 0 4rem 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: #f0f0f0;
}
.brands-title {
  color: #222;
  font-size: 2.5rem;
  font-weight: bold;
  text-align: center;
  margin-bottom: 2rem;
  width: 100%;
  letter-spacing: 0.5px;
}
.brands-slider-container {
  position: relative;
  width: 1400px;
  height: 300px;
  perspective: 1200px;
  margin: 0 auto;
  display: flex;
  align-items: center;
  justify-content: center;
}
.brands-slider-3d {
  width: 100%;
  height: 100%;
  position: absolute;
  left: 0;
  top: 0;
  transform-style: preserve-3d;
  transition: transform 0.8s cubic-bezier(0.4, 0, 0.2, 1);
}

.brand-slide {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 180px;
  height: 120px;
  margin: -60px 0 0 -90px;
  border-radius: 16px;
  box-shadow: 0 2px 12px rgba(0, 0, 0, 0.1);
  transition:
    transform 0.8s cubic-bezier(0.4, 0, 0.2, 1),
    box-shadow 0.2s;
  transform-style: preserve-3d;
  overflow: visible;
}
.brand-slide-front,
.brand-slide-back {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  border-radius: 16px;
  display: flex;
  align-items: center;
  justify-content: center;
  backface-visibility: hidden;
}
.brand-slide-front {
  background: #fff;
  z-index: 2;
}
.brand-slide-back {
  background: #000;
  transform: rotateY(180deg);
  z-index: 1;
}

.brand-img {
  max-width: 120px;
  max-height: 80px;
  object-fit: contain;
}
.brands-slider-btn {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background: #fff;
  border: none;
  border-radius: 50%;
  width: 40px;
  height: 40px;
  font-size: 1.5rem;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  cursor: pointer;
  z-index: 2;
  transition: background 0.2s;
}
.brands-slider-btn.prev {
  left: -60px;
}
.brands-slider-btn.next {
  right: -60px;
}
.brands-slider-btn:hover {
  background: #e0e0e0;
}
</style>

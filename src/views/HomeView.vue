<script setup lang="ts">
import { reactive, computed } from 'vue'
import brand1 from '/src/assets/brand-logo/axis.webp'
import brand2 from '@/assets/brand-logo/baldo.jpg'
import brand3 from '@/assets/brand-logo/bridgestone.png'
import brand4 from '@/assets/brand-logo/callaway.png'
import brand5 from '@/assets/brand-logo/epon.png'
import brand6 from '@/assets/brand-logo/honma.webp'
import brand7 from '@/assets/brand-logo/jbeam.png'
import brand8 from '@/assets/brand-logo/kotobuki.png'
import brand9 from '@/assets/brand-logo/kyoei.webp'
import brand10 from '@/assets/brand-logo/miura.png'
import brand11 from '@/assets/brand-logo/mizuno.png'
import brand12 from '@/assets/brand-logo/onoff.webp'
import brand13 from '@/assets/brand-logo/ryoma.jpg'
import brand14 from '@/assets/brand-logo/srixon.png'
import brand15 from '@/assets/brand-logo/taylormade.png'
import brand16 from '@/assets/brand-logo/titleist.png'
import brand17 from '@/assets/brand-logo/vega.png'
import brand18 from '@/assets/brand-logo/xxio.jpg'
import brand19 from '@/assets/brand-logo/yamaha.png'


// Brands 3D slider logic
const brands = [
  { name: 'Brand 1', img: brand1 },
  { name: 'Brand 2', img: brand2 },
  { name: 'Brand 3', img: brand3 },
  { name: 'Brand 4', img: brand4 },
  { name: 'Brand 5', img: brand5 },
  { name: 'Brand 6', img: brand6 },
  { name: 'Brand 7', img: brand7 },
  { name: 'Brand 8', img: brand8 },
  { name: 'Brand 9', img: brand9 },
  { name: 'Brand 10', img: brand10 },
  { name: 'Brand 11', img: brand11 },
  { name: 'Brand 12', img: brand12 },
  { name: 'Brand 13', img: brand13 },
  { name: 'Brand 14', img: brand14 },
  { name: 'Brand 15', img: brand15 },
  { name: 'Brand 16', img: brand16 },
  { name: 'Brand 17', img: brand17 },
  { name: 'Brand 18', img: brand18 },
  { name: 'Brand 19', img: brand19 }

]

const brandsState = reactive({ angle: 0 })
const totalBrands = brands.length
const radius = 1000 // px, distance from center

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
  transform: `rotateX(0deg) translateZ(-${radius}px)`,
}))

// In <script setup lang="ts">
import backgroundVideo from '@/assets/test-vid.mp4'



</script>

<template>
  <main>
    <div class="background-gallery-container">
      <div class="gallery-fade">
        <video autoplay loop muted playsinline class="background-video">
  <source :src="backgroundVideo" type="video/mp4" />
</video>


      </div>
      <div class="welcome-text">Welcome to Hikari</div>
    </div>

    <div class="products-section" id="products-section">
      <h2 class="products-title">Our Products</h2>
      <div class="products-container">
        <div class="product-card">
          <div class="product-image-container">
            <img src="/src/assets/cover.png" alt="Product 1" class="product-image" />
            <div class="product-title-overlay">Apparel &<br> Personal Gear</div>
          </div>
        </div>
        <div class="product-card">
          <div class="product-image-container">
            <img src="/src/assets/IMG_6650.png" alt="Product 2" class="product-image" />
            <div class="product-title-overlay">Accesories</div>
          </div>
        </div>
        <div class="product-card">
          <div class="product-image-container">
            <img src="/src/assets/IMG_6660.png" alt="Product 3" class="product-image" />
            <div class="product-title-overlay">Bags</div>
          </div>
        </div>
        <div class="product-card">
          <div class="product-image-container">
            <img src="/src/assets/IMG_6614.png" alt="Product 4" class="product-image" />
            <div class="product-title-overlay">Clubs</div>
          </div>
        </div>
        <div class="product-card">
          <div class="product-image-container">
            <img src="/src/assets/IMG_6617.png" alt="Product 5" class="product-image" />
            <div class="product-title-overlay">Aide</div>
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
            <div class="about-card-title">WHO WE ARE</div>
            <div class="about-card-text">
              <span style="font-weight: bold">HIKARI GOLF</span>, founded in May 2021, is a
              performance-first golf lifestyle brand redefining the game through cutting-edge
              design, inclusivity, and bold innovation. Built for modern athletes, we fuse technical
              function with elevated style—delivering gear that performs as hard as you do, on and
              off the course. Inspired by the Japanese word “Hikari,” meaning “light,” we aim to
              lead the next era of golf—honoring the sport’s heritage while driving it forward with
              purpose and precision.
            </div>
          </div>
        </div>
        <!-- Mission -->
        <div class="about-card mission">
          <div class="about-card-image left">
            <img src="/src/assets/cover.png" class="about-image" alt="Mission" />
          </div>
          <div class="about-card-content">
            <div class="about-card-title">Mission</div>
            <div class="about-card-text">
              Our mission is to empower every golfer to perform with confidence, express their
              individuality, and pursue excellence—on and off the course. We craft premium apparel,
              high-performance equipment, and unforgettable experiences that elevate both play and
              lifestyle.
            </div>
          </div>
        </div>
        <!-- Vision -->
        <div class="about-card vision">
          <div class="about-card-content">
            <div class="about-card-title">Vision</div>
            <div class="about-card-text">
              To lead the evolution of modern golf culture—where performance meets elegance,
              diversity drives progress, and a bold new standard lights the path for the next
              generation of players.
            </div>
          </div>
          <div class="about-card-image right">
            <img src="/src/assets/IMG_6650.png" class="about-image" alt="Vision" />
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
      <h2 class="contact-title">Pre-Order Now</h2>
      <p>Reserve Yours Now</p>
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
  </main>
</template>
<style scoped>

/* Our Products container styles */
.products-section {
  width: 100%;
  height: 300px;

  background: transparent;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 0 100px 0 100px;
  background-color: white;
}
.products-section .products-title {
  color: black;
  font-size: 2rem;
  font-weight: bold;
  background-color: transparent;
}
.products-container {
  display: flex;
  gap: 1.5rem;
  width: 100%;
  justify-content: center;
  padding: 20px;
}
.product-card {
  width: 200px;
  height: 200px;
  overflow: hidden;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 10px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1); /* Softer shadow */
  border-radius: 10px;
  transition:
    box-shadow 0.3s ease,
    transform 0.3s ease;
}

.product-card:hover {
  box-shadow: 0 12px 28px rgba(0, 0, 0, 0.25); /* Stronger shadow on hover */
  transform: scale(1.05);
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
  border-radius: 10px;
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
  line-height: 1;
}
/* Background gallery container styles */
.background-gallery-container {
  width: 100%;
  height: 400px;
  margin-top: 80px;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  background: #181818; /* fallback background, adjust as needed */
  overflow: hidden;
}
.background-video {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
  z-index: 0;
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
.about-section {
  width: 100%;
  padding: 0 100px 0 100px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: white;
}
.about-title {
  color: black;
  font-size: 2.5rem;
  font-weight: bold;
  text-align: center;
  width: 100%;
  letter-spacing: 0.5px;
}
.about-containers {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  padding: 0;
  margin: 0;
}
.about-card {
  width: 100%;
  overflow: hidden;
  display: flex;
  flex-direction: row;
  align-items: center;
}
.about-card-title {
  font-size: 2rem;
  font-weight: bold;
  color: #000;
}
.who-are-we {
  text-align: center;
  justify-content: center;
  margin: 0 0 10px 0;
  padding: 0 125px 0 125px;
  color: #000;
}
.mission {
  background-color: #f5eeda;
  height: 200px;
  margin: 10px 0 10px 0;
  color:#000;
}
.vision {
  background-color: #f5eeda;
  height: 200px;
  margin: 10px 0 10px 0;
  color:#000;
}
.about-card-image {
  width: 70%;
  height: 100%;
  overflow: hidden;
}
.about-image {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}
.about-card-content {
  width: 100%;
  height: 100%;
  margin: 0;
  padding: 0 75px;

  display: flex;
  flex-direction: column;
  justify-content: center; /* centers horizontally */
  align-items: left; /* centers vertically */
  /* centers inline text inside elements like <p> or <span> */
}

/* Contact Section Styles */
.contact-section {
  width: 100%;
  padding: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: white;
  padding: 20px 0 20px 0;
}
.contact-title {
  color: #222;
  font-size: 2.5rem;
  font-weight: bold;
  text-align: center;
  width: 100%;
  letter-spacing: 0.5px;
  line-height: 1;
}
.contact-section p {
  color: black;
  font-weight: bold;
}
.contact-containers {
  display: flex;
  flex-direction: row;
  justify-content: center;
  align-items: stretch;
  gap: 2rem;
  width: 100%;
  max-width: 900px;
  padding: 100px;
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
  padding: 0 100px 0 100px;
  display: flex;
  flex-direction: column;
  align-items: center;
  background: white;
}
.brands-title {
  color: #000;
  font-size: 2.5rem;
  font-weight: bold;
  text-align: center;
  width: 100%;
  letter-spacing: 0.5px;
}
.brands-slider-container {
  position: relative;
  width: 100%;
  height: 300px;
  perspective: 1200px;
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
  width: 300px;
  height: 150px;
  margin: -75px 0 0 -150px;
  border-radius: 16px;
  box-shadow: 0 0 30px rgba(0, 0, 0, 0.25);
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
</style>

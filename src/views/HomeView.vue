<script setup lang="ts">
//import brands
import brand1 from '@/assets/brand-logo/axis.webp'
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


const brands = [
  { name: 'Axis', img: brand1 },
  { name: 'Baldo', img: brand2 },
  { name: 'Bridgestone', img: brand3 },
  { name: 'Callaway', img: brand4 },
  { name: 'Epon', img: brand5 },
  { name: 'Honma', img: brand6 },
  { name: 'JBeam', img: brand7 },
  { name: 'Kotobuki', img: brand8 },
  { name: 'Kyoei', img: brand9 },
  { name: 'Miura', img: brand10 },
  { name: 'Mizuno', img: brand11 },
  { name: 'OnOff', img: brand12 },
  { name: 'Ryoma', img: brand13 },
  { name: 'Srixon', img: brand14 },
  { name: 'TaylorMade', img: brand15 },
  { name: 'Titleist', img: brand16 },
  { name: 'Vega', img: brand17 },
  { name: 'XXIO', img: brand18 },
  { name: 'Yamaha', img: brand19 }
]



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

    <div class="products-section-cat" id="products-section-cat">
      <h2 class="products-title-cat">Our Products</h2>
      <div class="products-container-cat">
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/cover.png" alt="Product 1" class="product-image-cat" />
            <div class="product-title-overlay-cat">Apparel &<br> Personal Gear</div>
          </div>
        </div>
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/IMG_6650.png" alt="Product 2" class="product-image-cat" />
            <div class="product-title-overlay-cat">Accesories</div>
          </div>
        </div>
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/IMG_6660.png" alt="Product 3" class="product-image-cat" />
            <div class="product-title-overlay-cat">Bags</div>
          </div>
        </div>
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/IMG_6614.png" alt="Product 4" class="product-image-cat" />
            <div class="product-title-overlay-cat">Clubs</div>
          </div>
        </div>
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/IMG_6617.png" alt="Product 5" class="product-image-cat" />
            <div class="product-title-overlay-cat">Aide</div>
          </div>
        </div>

      </div>
    </div>

    <!-- About Section -->
    <section class="about-section" id="about-section">
      <div class="about-containers">
        <!-- WHO ARE WE -->
        <div class="about-card who-are-we">
          <div class="about-card-content">
            <div class="about-card-title"><h2>WHO WE ARE</h2></div>
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
            <div class="about-card-title"><h2>Mission</h2></div>
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
            <div class="about-card-title"><h2>Vision</h2></div>
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
    <section class="brand-container">
    <h2 class="brand-title">Our Brands</h2>
    <div class="brand-grid">
      <div v-for="(brand, index) in brands" :key="index" class="brand-card">
        <img :src="brand.img" :alt="brand.name" class="brand-image" />
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


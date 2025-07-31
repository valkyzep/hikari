<script setup lang="ts">
import { onMounted, nextTick } from 'vue'
import { useRoute } from 'vue-router'

const route = useRoute()

onMounted(() => {
  if (route.hash) {
    nextTick(() => {
      const el = document.querySelector(route.hash)
      if (el) {
        setTimeout(() => {
          el.scrollIntoView({ behavior: 'smooth' })
        }, 100) // Allow a tiny delay for layout/render
      }
    })
  }
})


//import brands
const brandList = [
  { name: 'Axis', file: 'axis.webp' },
  { name: 'Baldo', file: 'baldo.jpg' },
  { name: 'Bridgestone', file: 'bridgestone.png' },
  { name: 'Callaway', file: 'callaway.png' },
  { name: 'Epon', file: 'epon.png' },
  { name: 'Honma', file: 'honma.webp' },
  { name: 'JBeam', file: 'jbeam.png' },
  { name: 'Kotobuki', file: 'kotobuki.png' },
  { name: 'Kyoei', file: 'kyoei.webp' },
  { name: 'Miura', file: 'miura.png' },
  { name: 'Mizuno', file: 'mizuno.png' },
  { name: 'OnOff', file: 'onoff.webp' },
  { name: 'Ryoma', file: 'ryoma.jpg' },
  { name: 'Srixon', file: 'srixon.png' },
  { name: 'TaylorMade', file: 'taylormade.png' },
  { name: 'Titleist', file: 'titleist.png' },
  { name: 'Vega', file: 'vega.png' },
  { name: 'XXIO', file: 'xxio.jpg' },
  { name: 'Yamaha', file: 'yamaha.png' },
  { name: 'Ping', file: 'ping.png' }
]

const brands = brandList.map(({ name, file }) => ({
  name,
  img: new URL(`/src/assets/brand-logo/${file}`, import.meta.url).href
}))



</script>

<template>
  <main>
    <div class="background-gallery">
    <div
  v-for="(brand, i) in brands"
  :key="i"
  class="slide"
  :style="{
    backgroundImage: `url(${brand.img})`,
    animationDelay: `${i * 4}s`
  }"
></div>


  </div>



    <div class="products-section-cat" id="products-section-cat">
      <h2 class="products-title-cat">PRODUCTS</h2>
      <div class="products-container-cat">
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/GOLFICONS/CLUBS-ICON.png" alt="Product 1" class="product-image-cat" />
          </div>
          <div class="product-title-card-cat">CLUBS</div>
        </div>
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/GOLFICONS/APPARELICON.png" alt="Product 2" class="product-image-cat" />
          </div>
          <div class="product-title-card-cat">APPARELS</div>
        </div>
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/GOLFICONS/GOLFBAGSICON.png" alt="Product 3" class="product-image-cat" />
          </div>
          <div class="product-title-card-cat">BAGS</div>
        </div>
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/GOLFICONS/AIDEICON.png" alt="Product 4" class="product-image-cat" />
          </div>
          <div class="product-title-card-cat">AIDE</div>
        </div>
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/GOLFICONS/ACCESSORIESICON.png" alt="Product 5" class="product-image-cat" />
          </div>
          <div class="product-title-card-cat">ACCESSORIES</div>
        </div>

      </div>
    </div>
    <!-- Brands We Carry Section -->
    <section class="brand-container">
      <div class="our-brands">
        <h2 class="brand-title">OUR BRANDS</h2>
        <div class="brand-grid">
          <div v-for="(brand, index) in brands" :key="index" class="brand-card">
            <img :src="brand.img" :alt="brand.name" class="brand-image" />
          </div>
        </div>
      </div>
    </section>


    <!-- Contact Section -->
    <section class="contact-section" id="contact-section">
      <div class="con-sec">
      <h2 class="contact-title">PRE-ORDER NOW</h2>
      <div class="contact-containers">
  <div class="contact-card facebook">
    <div class="contact-icon">
      <svg
        width="100"
        height="100"
        viewBox="0 0 24 24"
        fill="white"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M22.675 0h-21.35C.595 0 0 .595 0 1.326v21.348C0 23.405.595 24 1.326 24h11.495v-9.294H9.691v-3.622h3.13V8.413c0-3.1 1.893-4.788 4.659-4.788 1.325 0 2.463.099 2.797.143v3.24l-1.918.001c-1.504 0-1.797.715-1.797 1.763v2.313h3.587l-.467 3.622h-3.12V24h6.116C23.405 24 24 23.405 24 22.674V1.326C24 .595 23.405 0 22.675 0z"
        />
      </svg>
    </div>
  </div>

  <div class="contact-card instagram">
  <div class="contact-icon">
    <svg
      width="100"
      height="100"
      viewBox="0 0 420 470"
      fill="white"
      xmlns="http://www.w3.org/2000/svg"
    >
      <path d="M224.1 141c-63.6 0-115.1 51.5-115.1 115.1s51.5 115.1 115.1 115.1
        115.1-51.5 115.1-115.1S287.7 141 224.1 141zm0
        189.6c-41.1 0-74.5-33.4-74.5-74.5s33.4-74.5
        74.5-74.5 74.5 33.4 74.5 74.5-33.4 74.5-74.5
        74.5zm146.4-194.3c0 14.9-12 26.9-26.9
        26.9s-26.9-12-26.9-26.9 12-26.9 26.9-26.9
        26.9 12 26.9 26.9zm76.1 27.2c-1.7-35.7-9.9-67.3-36.2-93.5S391.8
        0 356.1 1.7c-35.7-1.7-143.3-1.7-179
        0-35.7-1.7-67.3 9.9-93.5 36.2S0 120.2
        1.7 155.9c-1.7 35.7-1.7 143.3
        0 179-1.7 35.7 9.9 67.3 36.2
        93.5s57.8 37.9 93.5 36.2c35.7 1.7 143.3
        1.7 179 0 35.7 1.7 67.3-9.9
        93.5-36.2s37.9-57.8 36.2-93.5c1.7-35.7
        1.7-143.3 0-179zM398.8 388c-7.8
        19.6-22.9 34.7-42.6 42.6-29.5 11.7-99.5
        9-132.1 9s-102.7 2.6-132.1-9c-19.6-7.8-34.7-22.9-42.6-42.6-11.7-29.5-9-99.5-9-132.1s-2.6-102.7
        9-132.1c7.8-19.6 22.9-34.7
        42.6-42.6 29.5-11.7 99.5-9 132.1-9s102.7-2.6
        132.1 9c19.6 7.8 34.7 22.9
        42.6 42.6 11.7 29.5 9 99.5
        9 132.1s2.7 102.7-9 132.1z"/>
    </svg>
  </div>
</div>

  <div class="contact-card telegram">
    <div class="contact-icon">
      <svg
        width="100"
        height="100"
        viewBox="0 0 24 24"
        fill="white"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M12 0C5.371 0 0 5.371 0 12c0 6.629 5.371 12 12 12s12-5.371 12-12c0-6.629-5.371-12-12-12zm5.707 7.293l-2.828 10.607c-.213.799-.771.992-1.562.617l-2.156-1.592-1.04 1.001c-.115.115-.211.211-.432.211l.155-2.197 7.995-7.211c.174-.155-.038-.242-.271-.087l-9.885 6.221-2.13-.664c-.776-.242-.792-.776.162-1.147l13.322-5.142c.623-.242 1.174.155.974 1.08z"
        />
      </svg>
    </div>
  </div>

  <div class="contact-card whatsapp">
    <div class="contact-icon">
      <svg
        width="100"
        height="100"
        viewBox="0 0 24 24"
        fill="white"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M20.52 3.48A11.93 11.93 0 0012 0C5.373 0 0 5.373 0 12c0 2.11.55 4.16 1.6 5.98L0 24l6.26-1.64A11.94 11.94 0 0012 24c6.627 0 12-5.373 12-12 0-3.19-1.24-6.19-3.48-8.52zM12 22c-1.85 0-3.66-.5-5.22-1.44l-.37-.22-3.72.98.99-3.62-.24-.38A9.94 9.94 0 012 12c0-5.52 4.48-10 10-10s10 4.48 10 10-4.48 10-10 10zm5.2-7.6c-.28-.14-1.65-.81-1.9-.9-.25-.09-.43-.14-.61.14-.18.28-.7.9-.86 1.08-.16.18-.32.2-.6.07-.28-.14-1.18-.44-2.25-1.4-.83-.74-1.39-1.65-1.55-1.93-.16-.28-.02-.43.12-.57.13-.13.28-.34.42-.51.14-.17.18-.29.28-.48.09-.19.05-.36-.02-.5-.07-.14-.61-1.47-.84-2.01-.22-.53-.45-.46-.62-.47-.16-.01-.36-.01-.56-.01-.19 0-.5.07-.76.34-.26.27-1 1-.99 2.43.01 1.43 1.03 2.81 1.18 3 .15.19 2.03 3.1 4.93 4.22.69.3 1.23.48 1.65.61.69.22 1.32.19 1.81.12.55-.08 1.65-.67 1.89-1.32.23-.65.23-1.2.16-1.32-.07-.12-.25-.19-.53-.33z"
        />
      </svg>
    </div>
  </div>
</div>
<div class="contact-number-text">
    <h3>CONTACT US HERE: </h3>
    <p>+1(234)567-8901</p>
</div>
      </div>
    </section>
  </main>
</template>


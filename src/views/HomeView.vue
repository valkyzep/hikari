<script setup lang="ts">
import { onMounted, nextTick } from 'vue'
import { useRoute } from 'vue-router'
import banner1 from '@/assets/Images/Banners/Banner1-Desktop.jpg'
import banner2 from '@/assets/Images/Banners/Banner2-Desktop.jpg'
import banner3 from '@/assets/Images/Banners/Banner3-Desktop.jpg'

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

interface Brand {
  name: string
  img: string
}

//import brands
const brandList = [
  { name: 'Titleist', file: 'Titleist.png' },
  { name: 'TourEdge', file: 'TourEdge.png' },
  { name: 'BenHogan', file: 'BenHogan.png' },
  { name: 'Honma', file: 'Honma.png' },
  { name: 'Kotobuki', file: 'Kotobuki.png' },
  { name: 'SunMountain', file: 'SunMountain.png' },

  { name: 'TaylorMade', file: 'TaylorMade.png' },
  { name: 'TourStriker', file: 'TourStriker.png' },
  { name: 'Odyssey', file: 'Odyssey.png' },
  { name: 'Bettinardi', file: 'Bettinardi.png' },
  { name: 'SkyCaddie', file: 'SkyCaddie.png' },
  { name: 'PXG', file: 'PXG.png' },

  { name: 'Wilson', file: 'Wilson.png' },
  { name: 'Bagboy', file: 'BagBoy.png' },
  { name: 'XX10', file: 'XX10.png' },
  { name: 'Cleveland', file: 'Cleveland.png' },
  { name: 'Clicgear', file: 'Clicgear.png' },
  { name: 'Lamkin', file: 'Lamkin.png' },

  { name: 'Ping', file: 'Ping.png' },
  { name: 'Srixon', file: 'Srixon.png' },
  { name: 'Bushnell', file: 'Bushnell.png' },
  { name: 'Mizuno', file: 'Mizuno.png' },
  { name: 'Callaway', file: 'Callaway.png' },

  { name: 'ScottyCameron', file: 'ScottyCameron.png' },
  { name: 'Ryoma', file: 'Ryoma.png' },
  { name: 'Miura', file: 'Miura.png' },
  { name: 'Bridgestone', file: 'Bridgestone.png' },
]

// Limit to max 30
const maxItems = 30
const trimmedBrands: Brand[] = brandList.slice(0, maxItems).map(({ name, file }) => ({
  name,
  img: new URL(`/src/assets/Images/Brands/${file}`, import.meta.url).href
}))
// Desired column sizes
const columnSizes = [6, 6, 6, 5, 4]
const brandColumns: Brand[][] = []

let start = 0
for (const size of columnSizes) {
  brandColumns.push(trimmedBrands.slice(start, start + size))
  start += size
}

</script>

<template>
  <main>
    <div class="background-gallery">
  <div class="slide" :style="{ backgroundImage: `url(${banner1})` }"></div>
    <div class="slide" :style="{ backgroundImage: `url(${banner2})` }"></div>
  <div class="slide" :style="{ backgroundImage: `url(${banner3})` }"></div>
</div>



    <div class="products-section-cat" id="products-section-cat">
      <h2 class="products-title-cat">PRODUCTS</h2>
      <div class="products-container-cat">
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/Images/Category/Catlogo-Clubs.png" alt="Product 1" class="product-image-cat" />
          </div>
          <div class="product-title-card-cat">CLUBS</div>
        </div>
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/Images/Category/Catlogo-Apparel.png" alt="Product 2" class="product-image-cat" />
          </div>
          <div class="product-title-card-cat">APPARELS</div>
        </div>
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/Images/Category/Catlogo-Bags.png" alt="Product 3" class="product-image-cat" />
          </div>
          <div class="product-title-card-cat">BAGS</div>
        </div>
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/Images/Category/Catlogo-Aide.png" alt="Product 4" class="product-image-cat" />
          </div>
          <div class="product-title-card-cat">AIDE</div>
        </div>
        <div class="product-card-cat">
          <div class="product-image-container-cat">
            <img src="/src/assets/Images/Category/Catlogo-Accessory.png" alt="Product 5" class="product-image-cat" />
          </div>
          <div class="product-title-card-cat">ACCESSORIES</div>
        </div>

      </div>
    </div>
    <!-- Brands We Carry Section -->
    <section class="brand-container">
    <h2 class="brand-title">OUR BRANDS</h2>
    <div class="brand-grid-columns">
      <div
        v-for="(column, colIndex) in brandColumns"
        :key="colIndex"
        class="brand-column"
      >
        <div
          v-for="(brand, rowIndex) in column"
          :key="rowIndex"
          class="brand-card"
        >
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
      <img src="/src/assets/Images/Socials/Soclogo-Facebook.png" />
    </div>
  </div>

  <div class="contact-card instagram">
  <div class="contact-icon">
    <img src="/src/assets/Images/Socials/Soclogo-Instagram.png" />
  </div>
</div>

  <div class="contact-card telegram">
    <div class="contact-icon">
      <img src="/src/assets/Images/Socials/Soclogo-Telegram.png" />
    </div>
  </div>

  <div class="contact-card whatsapp">
    <div class="contact-icon">
      <img src="/src/assets/Images/Socials/Soclogo-Whatsapp.png" />
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


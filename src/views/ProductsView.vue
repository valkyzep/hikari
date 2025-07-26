<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'
import searchIcon from '@/assets/search.jpg'
import img6655 from '@/assets/IMG_6655.png'

// Define product type
type Product = {
  id: number
  title: string
  price: string
  image: string
  gallery: string[]
  description: string
}

const icon = searchIcon

// Dummy products with gallery
const products = ref<Product[]>(
  Array.from({ length: 10 }, (_, i) => ({
    id: i + 1,
    title: `Product ${i + 1}`,
    price: '65,000 (slightly negotiable)',
    image: img6655,
    gallery: [img6655, img6655, img6655],
    description: `
  <ul>
    <li><p>2025 Model</p></li>
    <li><p>Brand New</p></li>
    <li><p>6i to Pw (5 pcs.)</p></li>
    <li><p>Strong lofted irons (7i is at 29 degrees of loft)</p></li>
    <li><p>Ns Pro 950 Neo Stiff Flex</p></li>
    <li><p>Very Forgiving Irons, good for Beginners and Novice Golfers</p></li>
    <li><p>SRP at Transview - Php 80k</p></li>
  </ul>
`,
  }))
)


// Selected product popup
const selectedProduct = ref<Product | null>(null)
const selectedIndex = computed(() =>
  products.value.findIndex(p => p.id === selectedProduct.value?.id)
)

// Popup navigation
function openPopup(product: Product) {
  selectedProduct.value = product
  activeGalleryImageIndex.value = 0
}

function closePopup() {
  selectedProduct.value = null
}

function goToNextProduct() {
  if (selectedIndex.value < products.value.length - 1) {
    selectedProduct.value = products.value[selectedIndex.value + 1]
  }
}

function goToPreviousProduct() {
  if (selectedIndex.value > 0) {
    selectedProduct.value = products.value[selectedIndex.value - 1]
  }
}



// Search icon toggle behavior
onMounted(() => {
  const toggleSearch = document.getElementById('toggleSearch') as HTMLElement | null
  const searchInput = document.getElementById('searchInput') as HTMLInputElement | null

  toggleSearch?.addEventListener('click', (e) => {
    e.stopPropagation()
    if (toggleSearch && searchInput) {
      toggleSearch.style.display = 'none'
      searchInput.classList.add('expanded')
      searchInput.focus()
    }
  })

  document.addEventListener('click', (e) => {
    const target = e.target as HTMLElement
    if (!target.closest('.products-search') && toggleSearch && searchInput) {
      searchInput.classList.remove('expanded')
      setTimeout(() => {
        toggleSearch.style.display = 'inline-block'
      }, 1000)
    }
  })
})

//image gallery active
const activeGalleryImageIndex = ref<number>(0)

</script>



<template>
  <div class="products-section">
    <div class="products-header">
      <h2>Hikari Products</h2>
      <p>Explore our products</p>
    </div>
    <div class="products-filter">
      <div class="products-search">
        <button id="toggleSearch" class="search-toggle">
          <img :src="icon" alt="Search" class="search-icon" />
        </button>
        <input type="text" id="searchInput" class="search-box" placeholder="Search products..." />
      </div>

      <div class="products-sort">
        <select class="products-gear-type">
          <option value="">All Gear Types</option>
          <option value="apparel">Apparel & Personal Gear</option>
          <option value="accessories">Accessories</option>
          <option value="bags">Bags</option>
          <option value="clubs">Clubs</option>
          <option value="aide">Aide</option>
        </select>
        <select class="products-brand">
          <option value="">All Brands</option>
          <option value="titleist">Titleist</option>
          <option value="callaway">Callaway</option>
          <option value="taylormade">TaylorMade</option>
          <option value="onoff">Onoff</option>
          <option value="axis">Axis</option>
          <option value="vega">Vega</option>
          <option value="epon">Epon</option>
          <option value="kotobuki">Kotobuki</option>
          <option value="ryoma">Ryoma</option>
          <option value="baldo">Baldo</option>
          <option value="miura">Miura</option>
          <option value="jbeam">JBeam</option>
          <option value="mizuno">Mizuno</option>
          <option value="honma">Honma</option>
          <option value="srixon">Srixon</option>
          <option value="xxio">XXIO</option>
          <option value="bridgestone">Bridgestone</option>
          <option value="yamaha">Yamaha</option>
          <option value="kyoei">Kyoei</option>
        </select>
        <select class="products-status">
          <option value="">All Status</option>
          <option value="on-hand">On-hand</option>
          <option value="pre-order">Pre-order</option>
        </select>
      </div>
    </div>
    <div class="products container">
  <div
    v-for="product in products"
    :key="product.id"
    class="products-card"
    @click="openPopup(product)"
  >
    <img :src="product.image" :alt="product.title" class="products-image" />
    <div class="products-details">
      <h2 class="products-title">{{ product.title }}</h2>
    </div>
  </div>
</div>

<!-- POPUP CONTAINER -->
<div v-if="selectedProduct" class="popup-overlay" @click.self="closePopup">
  <div class="popup-content">

    <!-- Left Column -->
<div class="popup-left popup-column">
  <h2 class="popup-title">{{ selectedProduct.title }}</h2>
  <p class="popup-price">₱{{ selectedProduct.price }}</p>
  <div
    class="popup-description"
    v-html="selectedProduct.description || '<p>This is a placeholder for more product details.</p>'"
  ></div>
  <div class="popup-contactus">
    <p>Can do meet-ups during weekends or in Pasig Area during weekdays.</p>
    <p>Can do shipping as well (Buyer to shoulder shipping fee).</p>
  </div>



  <!-- Bottom Controls -->
  <div class="popup-actions">
    <button class="product-button">Message Us Now</button>

    <div class="product-navigation">
      <button @click.stop="goToPreviousProduct">←</button>
      <button @click.stop="goToNextProduct">→</button>
    </div>
  </div>
</div>


    <!-- Right Column (Gallery) -->
<div class="popup-right popup-column">
  <!-- Active Image Preview -->
  <div class="active-image-preview">
    <img
      v-if="selectedProduct"
      :src="selectedProduct.gallery[activeGalleryImageIndex]"
      class="active-gallery-image"
      :alt="`Main preview image`"
    />
  </div>

  <!-- Gallery Thumbnails -->
  <div class="popup-gallery">
    <img
      v-for="(img, index) in selectedProduct.gallery"
      :key="index"
      :src="img"
      :alt="`Gallery image ${index + 1}`"
      class="gallery-thumb"
      :class="{ 'active-thumb': index === activeGalleryImageIndex }"
      @click="activeGalleryImageIndex = index"
    />
  </div>
</div>


    <!-- Close Button -->
    <button class="popup-close" @click="closePopup">✖</button>
  </div>


</div>


  </div>
</template>
<style scoped>
























































</style>
<style>






</style>


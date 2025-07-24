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
      <h1>Hikari Products</h1>
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
.products-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  text-align: center;
  padding: 25px 100px 100px 100px;
  margin-top: 80px;
  background-color: white;
}
.products-header {
  margin-bottom: 10px;
}
.products-header h1 {
  font-size: 2rem;
  font-weight: bold;
  line-height: 1;
  color: #000;
}
.products-header p {
  font-size: 1.2rem;
  color: #000;
  font-weight: 500;
}
.products-filter {
  display: flex;
  justify-content: space-between; /* left and right align */
  align-items: center;
  flex-wrap: wrap; /* allows wrapping on smaller screens */
  gap: 1rem;
  width: 100%;
  margin-bottom: 30px;
  background-color: white;
  padding: 0;
  height: 40px;

}

.products-search {
  display: flex;
  align-items: center;
  position: relative;
  background-color: white;
}
.search-icon {
  width: 30px;
  height: 30px;
  object-fit: contain;
}
.search-toggle {
  background: none;
  border: none;
  cursor: pointer;
  transition: opacity 1s ease;
  margin-right: 0.5rem;
}
.search-toggle.hide {
  opacity: 0;
  pointer-events: none;
}
.search-box {
  width: 0;
  opacity: 0;
  transition:
    width 1s ease,
    opacity 1.5s ease;
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-left: 0.5rem;
  overflow: hidden;
  pointer-events: none;
  height: 40px; /* ← Set your desired height here */
  box-sizing: border-box;
}
.products-search .search-box:focus {
  border-color: #007bff;
  outline: none;
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.25);
  background-color: #f9f9f9;
}
.search-box.expanded {
  width: 550px;
  opacity: 1;
  pointer-events: auto;
}
.search-box.expanded + .search-toggle {
  display: none;
}

.products-sort {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  justify-content: flex-end;
  align-items: flex-end;
  margin-top: auto; /* This is the key */
}

.products-sort select {
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
  height: 30px;
}
.products-sort select:focus {
  border-color: #007bff; /* Highlight border */
  outline: none; /* Remove default outline */
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.25); /* Soft glow effect */
  background-color: #f9f9f9; /* Optional: lighter background */
}
.products-gear-type:focus,
.products-brand:focus,
.products-status:focus {
  border-color: #007bff;
  outline: none;
  box-shadow: 0 0 0 3px rgba(0, 123, 255, 0.25);
  background-color: #f9f9f9;
}

.products.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(250px, 1fr));
  gap: 30px;
  width: 100%;
  padding: 0;
}
.products-card {
  background: #fff;
  border-radius: 10px;
  text-align: left;
  transition:
    transform 0.2s,
    box-shadow 0.2s;
  cursor: pointer;
  height: 250px;
  position: relative;
  overflow: hidden;

  /* Soft shadow */
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.products-card:hover {
  transform: scale(1.05);
  box-shadow: 0 8px 20px rgba(0, 0, 0, 0.15); /* Slightly stronger shadow on hover */
}

.products-image {
  width: 100%;
  height: 100%;
  border-radius: 10px;
  object-fit: cover;
}
.products-details {
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background: transparent; /* semi-transparent black background */
  color: #fff; /* white text for contrast */
  font-size: 0.875rem;
  transition: opacity 0.3s ease;
  opacity: 1;
  background: linear-gradient(to right, rgba(0, 0, 0, 0.6), transparent);
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 0.75rem 0 0.75rem;
}

.products-title {
  font-size: 1.5rem;
  font-weight: bold;
}
.products-price {
  font-size: 1.5rem;
  font-weight: bold;
}
.popup-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.6);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
  padding: 1rem;
  overflow: auto;
}

.popup-content {
  background: white;
  border-radius: 12px;
  padding: 2rem;
  display: flex;
  flex-wrap: wrap;
  gap: 2rem;
  width: 100%;
  width: 90vw;
  height: 80vh;
  overflow: auto;
  position: relative;
}

.popup-column {
  flex: 1 1 45%;
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;


}
.popup-left{
  padding: 0;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.popup-description{
  text-align: left;
  padding: 0 30px 0 30px;
}
.popup-actions {
  margin-top: auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.popup-right{
  padding:30px;
}
.popup-close {
  position: absolute;
  top: 0;
  right: 0;
  background: transparent;
  border: none;
  font-size: 2rem;
  font-weight: bold;
  cursor: pointer;
  color: #333;
}

.popup-title {
  font-size: 1.8rem;
  font-weight: 600;
  color: #111;
  text-align: left;
  background: linear-gradient(to right, gray, transparent);
  padding: 0 30px 0 30px;
  margin-top: 80px;

}

.popup-price {
  font-size: 1.4rem;
  color: #111;
  margin-bottom: 1rem;
  background: linear-gradient(to left, rgba(128, 128, 128, 0.4), rgba(128, 128, 128, 0));
  width: fit-content;
  padding: 0 30px 0 30px;
  text-align: right;
  margin-left: auto;
}
.popup-contactus{
  color:#000;
  text-align: left;
  padding: 10px 30px 0 30px;

}

.product-button {
  display: inline-block;
  background-color: #111;
  color: white;
  padding: 0.6rem 1.2rem;
  font-size: 1rem;
  border: none;
  border-radius: 6px;
  cursor: pointer;
  width: 300px;
}

.product-navigation {
  display: flex;
  gap: 1rem;
  justify-content: center;
}

.product-navigation button {
  font-size: 1.5rem;
  padding: 0.3rem 0.8rem;
  background: #eee;
  border: none;
  border-radius: 6px;
  cursor: pointer;
}
.product-navigation button {
  background-color: transparent;
  border: none;
  color: #000; /* Optional: change icon color */
  font-size: 1.5rem; /* Optional: make arrow larger */
  cursor: pointer;
}

.product-navigation button:hover {
  opacity: 0.7; /* Optional: hover effect */
}

/* Gallery thumbnail section */
.popup-gallery {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(80px, 1fr));
  gap: 1rem;
}

.gallery-thumb {
  width: 100%;
  aspect-ratio: 1 / 1;
  object-fit: cover;
  border-radius: 6px;
  cursor: pointer;
  transition: transform 0.2s ease;
}

.gallery-thumb:hover {
  transform: scale(1.05);
}
.active-image-preview {
  margin-bottom: 1.5rem;
  text-align: center;
}

.active-gallery-image {
  max-width: 100%;
  max-height: 100%;
  border-radius: 10px;
  object-fit: cover;
}

.active-thumb {
  border: 2px solid #333;
  transform: scale(1.05);
}



</style>
<style>
.popup-description ul {
  padding-left: 0;
  list-style: none;
  color: #000;
}

.popup-description li {
  position: relative;
  padding-left: 1.5rem;
  margin-bottom: 0.5rem;
  color: #000;
}

.popup-description li::before {
  content: '➤';
  position: absolute;
  left: 0;
  color: #000; /* Or any arrow color */
  font-size: 1rem;
}

.popup-description p {
  margin: 0;
  color: #000;

}

</style>


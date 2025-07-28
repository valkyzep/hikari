<script setup lang="ts">
import { ref, computed } from 'vue'
import img6655 from '@/assets/IMG_6655.png'

// Define product type
type Product = {
  id: number
  title: string
  price: string
  image: string
  gallery: string[]
  description: string
  gearType: string
  brand: string
  status: string
}

// Dummy products with gallery
const products = ref<Product[]>([
  {
    id: 1,
    title: 'Titleist T400 Iron Set',
    price: '37,000 (slightly negotiable)',
    image: img6655,
    gallery: [img6655, img6655, img6655],
    description: `
      <ul>
        <li><p>2021 Model and a Japan Release model</p></li>
        <li><p>In great condition</p></li>
        <li><p>7i to Pw, 43 Wedge and 49 Wedge (6pcs)</p></li>
        <li><p>Super strong lofted irons (7i is at 26 degrees of loft)</p></li>
        <li><p>NSPro Zelos 7 Shafts and Golf Pride Grips</p></li>
        <li><p>Good for Beginners and Novice players with slow downswing</p></li>
      </ul>
    `,
    gearType: 'clubs',
    brand: 'titleist',
    status: 'available',
  },
  {
    id: 2,
    title: 'Titleist Vokey SM10 Jet Black Wedge Set',
    price: '39,000 (slightly negotiable)',
    image: img6655,
    gallery: [img6655, img6655, img6655],
    description: `
      <ul>
        <li><p>2024 Model</p></li>
        <li><p>Brand New</p></li>
        <li><p>50, 54 and 58 Wedge Set</p></li>
        <li><p>NSPro BV 105 Shafts</p></li>
        <li><p>Plastics are still on the heads and grips</p></li>
        <li><p>SRP in Empire Golf - Php 14,000 per piece</p></li>
      </ul>
    `,
    gearType: 'clubs',
    brand: 'titleist',
    status: 'available',
  },
  {
    id: 3,
    title: 'Ryoma DSI Iron Set',
    price: '45,000 (slightly negotiable)',
    image: img6655,
    gallery: [img6655, img6655, img6655],
    description: `
      <ul>
        <li><p>2018 Model and a Japan Release model</p></li>
        <li><p>In great condition</p></li>
        <li><p>6i to Pw, Aw and Sw (7 pcs.)</p></li>
        <li><p>Strong lofted irons (7i is at 29 degrees of loft)</p></li>
        <li><p>Stock Ryoma Tour AD 57g R Flex Shafts and Stock Ryoma Grips</p></li>
        <li><p>Good for Seniors, Beginners and Novice players with slow downswing</p></li>
      </ul>
    `,
    gearType: 'clubs',
    brand: 'ryoma',
    status: 'available',
  },
  {
    id: 4,
    title: 'Titleist T350 Iron Set',
    price: '75,000 (slightly negotiable)',
    image: img6655,
    gallery: [img6655, img6655, img6655],
    description: `
      <ul>
        <li><p>2023 Model</p></li>
        <li><p>Brand New</p></li>
        <li><p>6i to Pw and 48 Wedge (6 pcs.)</p></li>
        <li><p>Strong lofted irons (7i is at 29 degrees of loft)</p></li>
        <li><p>Ns Pro 105T Stiff Flex Shafts</p></li>
        <li><p>Very Forgiving Irons</p></li>
        <li><p>SRP at Empire Golf - Php 113k</p></li>
      </ul>
    `,
    gearType: 'clubs',
    brand: 'titleist',
    status: 'available',
  },
  {
    id: 5,
    title: 'Ping G440 Iron Set',
    price: '70,000 (slightly negotiable)',
    image: img6655,
    gallery: [img6655, img6655, img6655],
    description: `
      <ul>
        <li><p>2025 Model</p></li>
        <li><p>Brand New</p></li>
        <li><p>6i to Pw, Uw (6 pcs.)</p></li>
        <li><p>Strong lofted irons (7i is at 29 degrees of loft)</p></li>
        <li><p>Ns Pro 950 Neo Stiff Flex</p></li>
        <li><p>Very Forgiving Irons, good for Beginners and Novice Golfers</p></li>
        <li><p>SRP at Golf Depot - Php 92k</p></li>
      </ul>
    `,
    gearType: 'clubs',
    brand: 'ping',
    status: 'available',
  },
  {
    id: 6,
    title: 'Callaway Elyte Iron Set',
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
    gearType: 'clubs',
    brand: 'callaway',
    status: 'available',
  },
  {
    id: 7,
    title: 'Callaway Elyte MAx Fast Iron Set',
    price: '65,000 (slightly negotiable)',
    image: img6655,
    gallery: [img6655, img6655, img6655],
    description: `
      <ul>
        <li><p>2025 Model</p></li>
        <li><p>Brand New</p></li>
        <li><p>6i to Pw (5 pcs.)</p></li>
        <li><p>Strong lofted irons (7i is at 30 degrees of loft)</p></li>
        <li><p>Ns Pro Zelos 7 Stiff Flex</p></li>
        <li><p>Very Forgiving Irons, good for Beginners and Novice Golfers</p></li>
        <li><p>SRP at Transview - Php 80k</p></li>
      </ul>
    `,
    gearType: 'clubs',
    brand: 'callaway',
    status: 'available',
  },
  {
    id: 8,
    title: 'Miura Giken CB-2008 Iron Set',
    price: '40,000 (slightly negotiable)',
    image: img6655,
    gallery: [img6655, img6655, img6655],
    description: `
      <ul>
        <li><p>2019 Model and a Japan Release model</p></li>
        <li><p>In great condition</p></li>
        <li><p>5i to Pw (6 pcs.)</p></li>
        <li><p>Tradionally lofted irons (7i is at 32 degrees of loft)</p></li>
        <li><p>NSPro Modus 105g Regular Flex/p></li>
        <li><p>With Susas Japan Grip</p></li>
        <li><p>Very forgiving Irons</p></li>
        <li><p>Great for beginners</p></li>
      </ul>
    `,
    gearType: 'clubs',
    brand: 'miura',
    status: 'available',
  },
])

// Filter state
const selectedGearType = ref('')
const selectedBrand = ref('')
const selectedStatus = ref('')

// Computed filtered products
const filteredProducts = computed(() => {
  return products.value.filter((product) => {
    const gearMatch = !selectedGearType.value || product.gearType === selectedGearType.value
    const brandMatch = !selectedBrand.value || product.brand === selectedBrand.value
    const statusMatch = !selectedStatus.value || product.status === selectedStatus.value
    return gearMatch && brandMatch && statusMatch
  })
})


// Popup state
const selectedProduct = ref<Product | null>(null)
const activeGalleryImageIndex = ref<number>(0)

// Popup navigation
function openPopup(product: Product) {
  selectedProduct.value = product
  activeGalleryImageIndex.value = 0
}

function closePopup() {
  selectedProduct.value = null
}
</script>




<template>
  <div class="products-section">
    <div class="products-header">
      <h2>Hikari Products</h2>
      <p>Explore our products</p>
    </div>
    <div class="products-filter">
      <div class="products-sort">
        <select class="products-gear-type" v-model="selectedGearType">
          <option value="">All Gear Types</option>
          <option value="apparel">Apparel & Personal Gear</option>
          <option value="accessories">Accessories</option>
          <option value="bags">Bags</option>
          <option value="clubs">Clubs</option>
          <option value="aide">Aide</option>
        </select>
        <select class="products-brand" v-model="selectedBrand">
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
          <option value="ping">Ping</option>
        </select>
        <select class="products-status" v-model="selectedStatus">
          <option value="">Product Status</option>
          <option value="available">Available</option>
          <option value="pre-order">Pre-order</option>
        </select>
      </div>
    </div>

<!-- Product Grid -->
    <div class="products container">
      <div
        v-for="product in filteredProducts"
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
    class="popup-description" v-html="selectedProduct.description">
  </div>

  <div class="popup-contactus">
    <p>Can do meet-ups during weekends or in Pasig Area during weekdays.</p>
    <p>Can do shipping as well (Buyer to shoulder shipping fee).</p>
  </div>
  <!-- Bottom Controls -->
  <div class="popup-actions">
    <button class="product-button">Message Us Now</button>
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

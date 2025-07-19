<script lang="ts">
import searchIcon from '@/assets/search.jpg'

export default {
  data() {
    return {
      searchIcon,
    }
  },
  mounted() {
    const toggleSearch = document.getElementById('toggleSearch') as HTMLElement
    const searchInput = document.getElementById('searchInput') as HTMLInputElement

    toggleSearch.addEventListener('click', (e) => {
      e.stopPropagation()
      toggleSearch.style.display = 'none'
      searchInput.classList.add('expanded')
      searchInput.focus()
    })

    document.addEventListener('click', (e) => {
      const target = e.target as HTMLElement
      if (!target.closest('.products-search')) {
        searchInput.classList.remove('expanded')
        // Wait for the collapse animation before showing the icon again
        setTimeout(() => {
          toggleSearch.style.display = 'inline-block'
        }, 1000) // match with CSS transition duration
      }
    })
  },
}
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
          <img :src="searchIcon" alt="Search" class="search-icon" />
          Search
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
      <div class="products-card">
        <img src="/src/assets/IMG_6655.png" alt="Product 1" class="products-image" />
        <div class="products-details">
          <h2 class="products-title">Product 1</h2>
          <h2 class="products-price">$100</h2>
        </div>
      </div>
      <div class="products-card">
        <img src="/src/assets/IMG_6655.png" alt="Product 2" class="products-image" />
        <div class="products-details">
          <h2 class="products-title">Product 2</h2>
          <h2 class="products-price">$100</h2>
        </div>
      </div>
      <div class="products-card">
        <img src="/src/assets/IMG_6655.png" alt="Product 3" class="products-image" />
        <div class="products-details">
          <h2 class="products-title">Product 3</h2>
          <h2 class="products-price">$100</h2>
        </div>
      </div>
      <div class="products-card">
        <img src="/src/assets/IMG_6655.png" alt="Product 4" class="products-image" />
        <div class="products-details">
          <h2 class="products-title">Product 4</h2>
          <h2 class="products-price">$100</h2>
        </div>
      </div>
      <div class="products-card">
        <img src="/src/assets/IMG_6655.png" alt="Product 5" class="products-image" />
        <div class="products-details">
          <h2 class="products-title">Product 5</h2>
          <h2 class="products-price">$100</h2>
        </div>
      </div>
      <div class="products-card">
        <img src="/src/assets/IMG_6655.png" alt="Product 6" class="products-image" />
        <div class="products-details">
          <h2 class="products-title">Product 6</h2>
          <h2 class="products-price">$100</h2>
        </div>
      </div>
      <div class="products-card">
        <img src="/src/assets/IMG_6655.png" alt="Product 7" class="products-image" />
        <div class="products-details">
          <h2 class="products-title">Product 7</h2>
          <h2 class="products-price">$100</h2>
        </div>
      </div>
      <div class="products-card">
        <img src="/src/assets/IMG_6655.png" alt="Product 8" class="products-image" />
        <div class="products-details">
          <h2 class="products-title">Product 8</h2>
          <h2 class="products-price">$100</h2>
        </div>
      </div>
      <div class="products-card">
        <img src="/src/assets/IMG_6655.png" alt="Product 9" class="products-image" />
        <div class="products-details">
          <h2 class="products-title">Product 9</h2>
          <h2 class="products-price">$100</h2>
        </div>
      </div>
      <div class="products-card">
        <img src="/src/assets/IMG_6655.png" alt="Product 10" class="products-image" />
        <div class="products-details">
          <h2 class="products-title">Product 10</h2>
          <h2 class="products-price">$100</h2>
        </div>
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
  margin-top: 100px;
  background-color: transparent;
}
.products-header {
  margin-bottom: 10px;
}
.products-header h1 {
  font-size: 2rem;
  font-weight: bold;
  line-height: 1;
}
.products-header p {
  font-size: 1.2rem;
  color: #666;
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
  background-color: transparent;
  padding: 0;
  height: 40px;
}

.products-search {
  display: flex;
  align-items: center;
  position: relative;
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
}

.products-sort select {
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
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
</style>

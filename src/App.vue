<script setup lang="ts">
import { ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import '@/assets/main.css'
import '@/assets/base.css'



const router = useRouter()
const route = useRoute()
const isOpen = ref(false)

const toggleMenu = () => {
  isOpen.value = !isOpen.value
}

// Scroll to specific section ID on the homepage
function goHomeAndScrollToSection(sectionId: string) {
  isOpen.value = false

  if (route.path !== '/') {
    router.push({ path: '/', hash: `#${sectionId}` })
  } else {
    // Already on home: manually scroll and update URL hash
    const el = document.getElementById(sectionId)
    if (el) {
      el.scrollIntoView({ behavior: 'smooth' })
      history.replaceState(null, '', `/#${sectionId}`)
    }
  }
}

// Scroll to top of page
function goHomeAndScrollTop() {
  isOpen.value = false

  // If already on home with hash (like /#about-section)
  if (route.path === '/' && route.hash) {
    router.replace({ path: '/', hash: '' }).then(() => {
      window.location.reload() // 💥 Force full reload with clean URL
    })
  }
  // If on home without hash
  else if (route.path === '/') {
    window.location.reload()
  }
  // If on another page
  else {
    router.push('/').then(() => {
      window.location.reload()
    })
  }
}

function closeMenu() {
  isOpen.value = false
}



</script>





<template>
  <header>
  <nav class="navbar">
    <a class="logo" href="#" @click.prevent="goHomeAndScrollTop"><img src="@/assets/Logo14.png" alt="Logo" class="navbar-logo" /></a>


    <!-- DESKTOP NAV -->
    <div class="navbar-tabs-desktop">
      <a href="#" @click.prevent="goHomeAndScrollTop">Home</a>
      <RouterLink to="/products">Products</RouterLink>
      <a href="#contact-section" @click.prevent="goHomeAndScrollToSection('contact-section')">Contact Us</a>
      <a href="#about-section" @click.prevent="goHomeAndScrollToSection('about-section')">About</a>

    </div>

    <!-- MOBILE HAMBURGER -->
    <button class="hamburger" :class="{ open: isOpen }" @click="toggleMenu" aria-label="Toggle navigation">
      <span></span>
      <span></span>
      <span></span>
    </button>

    <!-- MOBILE NAV -->
    <transition name="nav-fall">
      <div v-if="isOpen" class="navbar-tabs" @click.self="toggleMenu">
        <a href="#" @click.prevent="goHomeAndScrollTop">Home</a>
        <RouterLink to="/products" @click="closeMenu">Products</RouterLink>
        <a href="#contact-section" @click.prevent="goHomeAndScrollToSection('contact-section')">Contact Us</a>
        <a href="#about-section" @click.prevent="goHomeAndScrollToSection('about-section')">About</a>

      </div>
    </transition>
  </nav>
</header>


  <div class="main-content"><router-view /></div>

  <footer class="footer">
  <div class="footer-main">
    <!-- Left Column: Contact Info -->
    <div class="footer-col footer-contact-col">
      <span>Contact us:</span>
      <span>+1 (234) 567-8901</span>
    </div>

    <!-- Middle Column: Logo + Navigation -->
    <div class="footer-col footer-center-col">
      <img src="@/assets/Logo14.png" alt="Logo" class="footer-logo" />
      <nav class="footer-nav">
        <a href="#" @click.prevent="goHomeAndScrollTop">Home</a>
        <RouterLink to="/products">Products</RouterLink>
        <a href="#contact-section" @click.prevent="goHomeAndScrollToSection('contact-section')">Contact Us</a>
        <a href="#about-section" @click.prevent="goHomeAndScrollToSection('about-section')">About</a>

      </nav>
    </div>

    <!-- Right Column: Social Icons -->
    <div class="footer-col footer-social-col">
  <div class="footer-social">
    <a href="#" aria-label="Facebook"><i class="fab fa-facebook-f"></i></a>
    <a href="#" aria-label="Instagram"><i class="fab fa-instagram"></i></a>
    <a href="#" aria-label="Twitter"><i class="fab fa-twitter"></i></a>
  </div>
</div>

  </div>

  <div class="footer-credits">
    <span>© 2025 Your Company. All rights reserved.</span>
  </div>
</footer>



</template>



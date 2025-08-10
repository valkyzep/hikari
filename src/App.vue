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
    const el = document.getElementById(sectionId)
    if (el) {
      el.scrollIntoView({ behavior: 'smooth' })

      // ✅ Manually update the hash so route.hash updates
      router.replace({ path: '/', hash: `#${sectionId}` })
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
    <a class="logo" href="#" @click.prevent="goHomeAndScrollTop"><img src="@/assets/Images/Logohead.png" alt="Logo" class="navbar-logo" /></a>


    <!-- DESKTOP NAV -->
    <div class="navbar-tabs-desktop">
  <a
    href="#"
    @click.prevent="goHomeAndScrollTop"
    :class="{ active: route.path === '/' && !route.hash }"
  >HOME</a>

  <RouterLink
    to="/products"
    :class="{ active: route.path === '/products' }"
  >PRODUCTS</RouterLink>

  <a
    href="#contact-section"
    @click.prevent="goHomeAndScrollToSection('contact-section')"
    :class="{ active: route.hash === '#contact-section' }"
  >CONTACT US</a>
</div>

    <!-- MOBILE HAMBURGER -->
    <button class="hamburger" :class="{ open: isOpen }" @click="toggleMenu" aria-label="Toggle navigation">
      <span></span>
      <span></span>
      <span></span>
    </button>


  </nav>
</header>
<!-- MOBILE NAV -->
    <transition name="nav-fall">
      <div v-if="isOpen" class="navbar-tabs" @click.self="toggleMenu">
        <a href="#" @click.prevent="goHomeAndScrollTop">HOME</a>
        <RouterLink to="/products" @click="closeMenu">PRODUCTS</RouterLink>
        <a href="#contact-section" @click.prevent="goHomeAndScrollToSection('contact-section')">CONTACT US</a>

      </div>
    </transition>

  <div class="main-content"><router-view /></div>

  <footer class="footer">
  <div class="footer-main">
    <div class="footer-col footer-center-col">
      <img src="@/assets/Images/Logofooter.png" alt="Logo" class="footer-logo" />
    </div>
  </div>
  <div class="footer-credits">
    <span>© 2025 Your Company. All rights reserved.</span>
  </div>
</footer>



</template>



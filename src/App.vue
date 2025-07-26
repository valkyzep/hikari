<script setup lang="ts">
import { ref } from 'vue'
import { useRouter, useRoute } from 'vue-router'
import { RouterLink } from 'vue-router'
import '@/assets/main.css'
import '@/assets/base.css'


const router = useRouter()
const route = useRoute()
const isOpen = ref(false)

const toggleMenu = () => (isOpen.value = !isOpen.value)
const closeMenu = () => (isOpen.value = false)

function smoothScrollToElement(element: HTMLElement | null) {
  if (!element) return
  const headerOffset = 100
  const elementPosition = element.getBoundingClientRect().top + window.pageYOffset
  const offsetPosition = elementPosition - headerOffset

  const start = window.scrollY || window.pageYOffset
  const distance = offsetPosition - start
  const duration = 600
  let startTime: number | null = null

  function animation(currentTime: number) {
    if (startTime === null) startTime = currentTime
    const timeElapsed = currentTime - startTime
    const run = easeInOutQuad(timeElapsed, start, distance, duration)
    window.scrollTo(0, run)
    if (timeElapsed < duration) requestAnimationFrame(animation)
    else window.scrollTo(0, offsetPosition)
  }

  function easeInOutQuad(t: number, b: number, c: number, d: number): number {
    t /= d / 2
    if (t < 1) return (c / 2) * t * t + b
    t--
    return (-c / 2) * (t * (t - 2) - 1) + b
  }

  requestAnimationFrame(animation)
}

function goHomeAndScrollTop() {
  closeMenu()
  if (route.path !== '/') {
    router.push('/').then(() => {
      window.scrollTo({ top: 0, behavior: 'smooth' })
    })
  } else {
    window.scrollTo({ top: 0, behavior: 'smooth' })
  }
}

function goHomeAndScrollToContact() {
  closeMenu()
  if (route.path !== '/') {
    router.push('/').then(() => {
      setTimeout(() => {
        const section = document.getElementById('contact-section')
        if (section) smoothScrollToElement(section)
      }, 300)
    })
  } else {
    const section = document.getElementById('contact-section')
    if (section) smoothScrollToElement(section)
  }
}

function goHomeAndScrollToAbout() {
  closeMenu()
  if (route.path !== '/') {
    router.push('/').then(() => {
      setTimeout(() => {
        const section = document.getElementById('about-section')
        if (section) smoothScrollToElement(section)
      }, 300)
    })
  } else {
    const section = document.getElementById('about-section')
    if (section) smoothScrollToElement(section)
  }
}
</script>



<template>
  <header>
  <nav class="navbar">
    <img src="@/assets/Logo14.png" alt="Logo" class="navbar-logo" />

    <!-- DESKTOP NAV -->
    <div class="navbar-tabs-desktop">
      <a href="#" @click.prevent="goHomeAndScrollTop">Home</a>
      <RouterLink to="/products">Products</RouterLink>
      <a href="#contact-section" @click.prevent="goHomeAndScrollToContact">Contact Us</a>
      <a href="#about-section" @click.prevent="goHomeAndScrollToAbout">About</a>
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
        <RouterLink to="/products">Products</RouterLink>
        <a href="#contact-section" @click.prevent="goHomeAndScrollToContact">Contact Us</a>
        <a href="#about-section" @click.prevent="goHomeAndScrollToAbout">About</a>
      </div>
    </transition>
  </nav>
</header>


  <router-view />

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
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/products">Products</RouterLink>
        <RouterLink to="/contact">Contact Us</RouterLink>
        <a href="#about-section" @click.prevent="goHomeAndScrollToAbout">About</a>
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



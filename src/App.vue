<script setup lang="ts">
function smoothScrollToElement(element: HTMLElement | null) {
  if (!element) return
  const headerOffset = 100 // height of your fixed header
  const elementPosition = element.getBoundingClientRect().top + window.pageYOffset
  const offsetPosition = elementPosition - headerOffset
  const start = window.scrollY || window.pageYOffset
  const distance = offsetPosition - start
  const duration = 600
  let startTime: number | null = null

  function animation(currentTime: number) {
    if (startTime === null) startTime = currentTime
    const timeElapsed = currentTime - (startTime as number)
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
function goHomeAndScrollToContact() {
  if (route.path !== '/') {
    router.push('/').then(() => {
      setTimeout(() => {
        const contactSection = document.getElementById('contact-section')
        if (contactSection) smoothScrollToElement(contactSection)
      }, 300)
    })
  } else {
    const contactSection = document.getElementById('contact-section')
    if (contactSection) smoothScrollToElement(contactSection)
  }
}
function goHomeAndScrollToAbout() {
  if (route.path !== '/') {
    router.push('/').then(() => {
      setTimeout(() => {
        const aboutSection = document.getElementById('about-section')
        if (aboutSection) smoothScrollToElement(aboutSection)
      }, 300)
    })
  } else {
    const aboutSection = document.getElementById('about-section')
    if (aboutSection) smoothScrollToElement(aboutSection)
  }
}
import { RouterLink, useRouter, useRoute } from 'vue-router'

const router = useRouter()
const route = useRoute()
function goHomeAndScrollTop() {
  if (route.path !== '/') {
    router.push('/').then(() => {
      window.scrollTo({ top: 0, behavior: 'smooth' })
    })
  } else {
    window.scrollTo({ top: 0, behavior: 'smooth' })
  }
}
</script>

<template>
  <header>
    <nav class="navbar">
      <img src="@/assets/Logo14.png" alt="Logo" class="navbar-logo" width="32" height="32" />
      <div class="navbar-tabs">
        <a href="#" class="nav-tab" @click.prevent="goHomeAndScrollTop">Home</a>
        <RouterLink to="/products" class="nav-tab">Products</RouterLink>
        <a href="#contact-section" class="nav-tab" @click.prevent="goHomeAndScrollToContact"
          >Contact Us</a
        >
        <a href="#about-section" class="nav-tab" @click.prevent="goHomeAndScrollToAbout">About</a>
      </div>
    </nav>
  </header>
  <router-view />
  <section class="footer">
    <div class="footer-main">
      <div class="footer-col footer-col-left">
        <img src="@/assets/Logo14.png" alt="Logo" class="footer-logo" width="40" height="40" />
        <div class="footer-contact">
          <span>Contact us:</span>
          <span>+1 (234) 567-8901</span>
        </div>
      </div>
      <div class="footer-col footer-col-right">
        <nav class="footer-nav-vertical">
          <RouterLink to="/" class="nav-tab">Home</RouterLink>
          <RouterLink to="/products" class="nav-tab">Products</RouterLink>
          <RouterLink to="/contact" class="nav-tab">Contact Us</RouterLink>
          <a href="#about-section" class="nav-tab" @click.prevent="goHomeAndScrollToAbout">About</a>
        </nav>
        <div class="footer-social">
          <a href="#" aria-label="Facebook" class="footer-social-link">
            <svg
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M22.675 0h-21.35C.595 0 0 .595 0 1.326v21.348C0 23.405.595 24 1.326 24h11.495v-9.294H9.691v-3.622h3.13V8.413c0-3.1 1.893-4.788 4.659-4.788 1.325 0 2.463.099 2.797.143v3.24l-1.918.001c-1.504 0-1.797.715-1.797 1.763v2.313h3.587l-.467 3.622h-3.12V24h6.116C23.405 24 24 23.405 24 22.674V1.326C24 .595 23.405 0 22.675 0z"
                fill="#fff"
              />
            </svg>
          </a>
          <a href="#" aria-label="Twitter" class="footer-social-link">
            <svg
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M24 4.557a9.83 9.83 0 01-2.828.775 4.932 4.932 0 002.165-2.724c-.951.564-2.005.974-3.127 1.195a4.916 4.916 0 00-8.38 4.482C7.691 8.095 4.066 6.13 1.64 3.161c-.543.929-.855 2.006-.855 3.163 0 2.18 1.111 4.104 2.797 5.229a4.904 4.904 0 01-2.229-.616c-.054 2.281 1.581 4.415 3.949 4.89a4.936 4.936 0 01-2.224.084c.627 1.956 2.444 3.377 4.6 3.418A9.867 9.867 0 010 21.543a13.94 13.94 0 007.548 2.212c9.058 0 14.009-7.513 14.009-14.009 0-.213-.005-.425-.014-.636A10.025 10.025 0 0024 4.557z"
                fill="#fff"
              />
            </svg>
          </a>
          <a href="#" aria-label="Instagram" class="footer-social-link">
            <svg
              width="20"
              height="20"
              viewBox="0 0 24 24"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <path
                d="M12 2.163c3.204 0 3.584.012 4.85.07 1.366.062 2.633.334 3.608 1.308.975.974 1.246 2.242 1.308 3.608.058 1.266.07 1.646.07 4.85s-.012 3.584-.07 4.85c-.062 1.366-.334 2.633-1.308 3.608-.974.975-2.242 1.246-3.608 1.308-1.266.058-1.646.07-4.85.07s-3.584-.012-4.85-.07c-1.366-.062-2.633-.334-3.608-1.308-.975-.974-1.246-2.242-1.308-3.608C2.175 15.647 2.163 15.267 2.163 12s.012-3.584.07-4.85c.062-1.366.334-2.633 1.308-3.608.974-.975 2.242-1.246 3.608-1.308C8.416 2.175 8.796 2.163 12 2.163zm0-2.163C8.741 0 8.332.013 7.052.072 5.775.131 4.602.396 3.635 1.363c-.967.967-1.232 2.14-1.291 3.417C2.013 8.332 2 8.741 2 12c0 3.259.013 3.668.072 4.948.059 1.277.324 2.45 1.291 3.417.967.967 2.14 1.232 3.417 1.291C8.332 23.987 8.741 24 12 24s3.668-.013 4.948-.072c1.277-.059 2.45-.324 3.417-1.291.967-.967 1.232-2.14 1.291-3.417.059-1.28.072-1.689.072-4.948 0-3.259-.013-3.668-.072-4.948-.059-1.277-.324-2.45-1.291-3.417-.967-.967-2.14-1.232-3.417-1.291C15.668.013 15.259 0 12 0zm0 5.838A6.162 6.162 0 005.838 12 6.162 6.162 0 0012 18.162 6.162 6.162 0 0018.162 12 6.162 6.162 0 0012 5.838zm0 10.162A4 4 0 118 12a4 4 0 014 4zm6.406-11.845a1.44 1.44 0 11-2.88 0 1.44 1.44 0 012.88 0z"
                fill="#fff"
              />
            </svg>
          </a>
        </div>
      </div>
    </div>
    <div class="footer-credits">
      <span>© 2025 Your Company. All rights reserved.</span>
    </div>
  </section>
</template>

<style scoped>
html,
body {
  height: 100%;
  width: 100%;
  max-width: 100vw;
  overflow-x: hidden;
  margin: 0;
  padding: 0;
  background-color: white;
}

#app {
  min-height: 100vh;
}

.footer {
  width: 100vw;
  max-width: 100vw;
  overflow-x: hidden;
}

body {
  scrollbar-width: none; /* Firefox */
}

body::-webkit-scrollbar {
  display: none; /* Chrome, Safari, Opera */
}
header {
  width: 100vw;
  height: 80px;
  position: fixed;
  top: 0;
  left: 0;
  padding: 0.5rem 2rem;
  z-index: 100;
  background: #000;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.03);
}
nav.navbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  text-align: left;
  margin-left: 0;
}
/* Navbar styles unified for RouterLink and anchor tags */
.navbar-tabs {
  display: flex;
  align-items: center;
}
.navbar-logo {
  margin: 0 2rem 0 1rem;
  height: 82px;
  width: 175px;
  padding: 0px;
}
/* Unified navbar tab styles */
.nav-tab {
  margin: 0 1rem;
  text-decoration: none;
  color: #fff;
  font-size: 1rem;
  opacity: 0.85;
  transition:
    opacity 0.2s,
    font-weight 0.2s;
}
.nav-tab:hover,
.nav-tab.active {
  opacity: 1;
  font-weight: bold;
}
.footer {
  width: 100vw;
  position: static;
  left: 0;
  bottom: 0;
  z-index: 0;
}
.footer-main {
  background: #222;
  color: #fff;
  display: flex;
  flex-direction: row;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 2rem;
  min-height: 135px;
}
.footer-col {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}
.footer-col-left {
  align-items: flex-start;
  margin-left: 15rem;
}
.footer-col-right {
  align-items: flex-end;
  margin-right: 15rem;
}
.footer-logo {
  margin-bottom: 0.5rem;
  border-radius: 6px;
  height: 85px;
  width: 200px;
}
.footer-nav-vertical {
  display: flex;
  flex-direction: row;
  gap: 0;
  align-items: center;
  width: 200px;
  justify-content: space-between;
  padding: 0;
  margin: 0;
}
/* Footer nav unified styles */
/* Unified footer nav tab styles */
.footer-nav-vertical .nav-tab {
  color: #fff;
  font-size: 0.65rem;
  text-decoration: none;
  opacity: 0.8;
  padding: 0;
  margin: 0;
  transition:
    opacity 0.2s,
    font-weight 0.2s;
}
.footer-nav-vertical .nav-tab:hover,
.footer-nav-vertical .nav-tab.active {
  opacity: 1;
  font-weight: bold;
}
.footer-col-right {
  align-items: flex-end;
  justify-content: space-between;
}
.footer-social {
  display: flex;
  flex-direction: row;
  gap: 0.5rem;
  margin-bottom: 1rem;
}
.footer-social-link {
  background: transparent;
  color: #fff;
  border-radius: 50%;
  width: 32px;
  height: 32px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 1rem;
  text-decoration: none;
  opacity: 0.7;
  transition:
    background 0.2s,
    opacity 0.2s,
    transform 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.footer-social-link:hover {
  transform: translateY(-8px);
}

.footer-contact {
  display: flex;
  flex-direction: column;
  color: #fff;
  font-size: 0.95rem;
  margin: 0;
  padding: 0;
}
.footer-contact span {
  width: 100%;
  line-height: 1rem;
  margin: 0;
  padding: 0;
}

.footer-credits {
  background: #000;
  color: #fff;
  text-align: center;
  padding: 0.5rem 0;
  font-size: 0.9rem;
}
</style>

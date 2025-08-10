<template>
  <nav class="navbar sticky-top bg-light border-bottom" aria-label="Primary">
    <a class="skip-link" href="#main">Skip to content</a>

    <div class="container-fluid d-flex justify-content-center">
      <ul class="navbar-nav flex-row gap-2 gap-md-3">
        <li class="nav-item">
          <a class="nav-link px-3 py-2" href="#landing" :aria-current="active === 'landing' ? 'page' : null">About</a>
        </li>
        <li class="nav-item">
          <a class="nav-link px-3 py-2" href="#projects" :aria-current="active === 'projects' ? 'page' : null">Works</a>
        </li>
        <li class="nav-item">
          <a class="nav-link px-3 py-2" href="#tools" :aria-current="active === 'tools' ? 'page' : null">Skills</a>
        </li>
        <li class="nav-item">
          <a class="nav-link px-3 py-2" href="#contacts" :aria-current="active === 'contacts' ? 'page' : null">Contact</a>
        </li>
      </ul>
    </div>
  </nav>
</template>

<script setup>
import { onMounted, onBeforeUnmount, ref } from 'vue'

const active = ref('')  // id of the section in view

// Optional: automatically set the active link as the user scrolls
onMounted(() => {
  const ids = ['landing', 'projects', 'tools', 'contacts']
  const sections = ids
    .map(id => document.getElementById(id))
    .filter(Boolean)

  const io = new IntersectionObserver(
    entries => {
      entries.forEach(e => {
        if (e.isIntersecting) active.value = e.target.id
      })
    },
    { rootMargin: '0px 0px -60% 0px', threshold: 0.1 }
  )

  sections.forEach(s => io.observe(s))
  onBeforeUnmount(() => io.disconnect())
})
</script>

<style scoped>
/* Keep your color scheme */
.nav-link {
  color: #333;
  transition: color 200ms ease;
  border-radius: 8px;
}
.nav-link:hover,
.nav-link[aria-current="page"] {
  color: #fb5607;
  background: rgba(251, 86, 7, 0.06);
}

/* Strong focus style */
.nav-link:focus-visible {
  outline: 2px solid #fb5607;
  outline-offset: 2px;
}

/* Skip link for keyboard users */
.skip-link {
  position: absolute;
  left: -9999px;
}
.skip-link:focus {
  left: 12px;
  top: 12px;
  background: #fff;
  padding: 8px 12px;
  border: 1px solid #ddd;
  border-radius: 6px;
  z-index: 1000;
}
</style>

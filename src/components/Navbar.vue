<template>
  <nav class="navbar sticky-top bg-light border-bottom" aria-label="Primary">

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

const active = ref('')  

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
.nav-link:focus-visible {
  outline: 2px solid #fb5607;
  outline-offset: 2px;
}
</style>

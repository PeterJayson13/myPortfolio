<template>
  <nav class="navbar bg-dark sticky-top border">
    <div class="container-fluid">
      <a class="navbar-brand ms-5" href="#landing">MyCapStone</a>
      <ul class="navbar-nav ms-auto d-flex flex-row me-5">
        <li class="nav-item me-3"><a class="nav-link" href="#landing">Home</a></li>
        <li class="nav-item me-3"><a class="nav-link" href="#projects">Project Gallery</a></li>
        <li class="nav-item me-3"><a class="nav-link" href="#tools">Tools & Framework</a></li>
        <li class="nav-item"><a class="nav-link" href="#contacts">Let's Connect!</a></li>
      </ul>
    </div>
  </nav>
</template>

<script>
	
</script>

<style scoped>
nav {
  background-color: black;
  border-radius: 25px;
}
.navbar-brand {
  color: #fb5607;
}
.nav-link {
  color: white;
  transition: color 0.3s ease;
}
.nav-link:hover {
  color: #fb5607;
}
</style>
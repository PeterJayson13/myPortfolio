<template>
  <div class="col-12 col-md-4 mb-4">
    <div class="card project-card h-100 shadow-sm bg-dark text-white">
      <a v-if="project.link" :href="project.link" target="_blank" rel="noopener" class="project-link">
        <div class="project-img-wrapper">
          <img
            :src="project.image"
            class="card-img-top project-img"
            :alt="`${project.title} screenshot`"
            loading="lazy"
          />
        </div>
      </a>
      <div class="card-body">
        <h6 class="card-title">
          <a v-if="project.link" :href="project.link" target="_blank" rel="noopener" class="text-white text-decoration-none">
            {{ project.title }}
          </a>
          <span v-else>{{ project.title }}</span>
        </h6>
        <p class="card-text small text-white">{{ project.description }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
const { project } = defineProps({
  project: {
    type: Object,
    required: true
  }
});
</script>

<style scoped>
.project-card {
  border: 1px solid #e5e5e5;
  border-radius: 8px;
  transition: transform 0.15s ease, box-shadow 0.15s ease;
  background-color: #212529;
}
.project-card:hover {
  transform: translateY(-4px);
  box-shadow: 0 6px 16px rgba(0,0,0,0.1);
}

/* Keep all project images same small size without cropping important parts */
.project-img-wrapper {
  width: 100%;
  height: 120px; /* fixed height for uniformity */
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #f8f9fa;
}
.project-img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain; /* prevent cutoff */
}

.card-title {
  font-size: 1rem;
  margin-bottom: 0.5rem;
}
.card-text {
  color: #555;
}
</style>

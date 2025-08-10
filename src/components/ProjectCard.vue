<template>
  <div class="col-12 col-md-4 mb-4">
    <article class="card project-card h-100 shadow-sm bg-dark text-white">
      <div class="project-img-wrapper">
        <img
          :src="project.image"
          class="card-img-top project-img"
          :alt="`${project.title} screenshot`"
          loading="lazy"
          decoding="async"
        />
      </div>

      <div class="card-body d-flex flex-column">
        <h6 class="card-title mb-2">{{ project.title }}</h6>
        <p class="card-text small text-white-50 mb-3">{{ project.description }}</p>

        <!-- Actions -->
        <div class="mt-auto">
          <!-- External link -->
          <a
            v-if="project.link && isExternal"
            :href="project.link"
            target="_blank"
            rel="noopener"
            class="btn btn-sm btn-view-project"
            aria-label="View project [opens in new tab]"
          >
            View project
          </a>

          <RouterLink
            v-else-if="project.link"
            :to="project.link"
            class="btn btn-sm btn-light"
            aria-label="View project"
          >
            View project
          </RouterLink>
        </div>
      </div>
    </article>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const { project } = defineProps({
  project: {
    type: Object,
    required: true
  }
})

const isExternal = computed(() =>
  typeof project.link === 'string' && /^https?:\/\//i.test(project.link)
)
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
.btn-view-project{
  background-color: #fb5607;
  color: #fff;
  border: 1px solid #fb5607;
  border-radius: 8px;
  padding: 8px 12px;
  transition: background-color 150ms ease, border-color 150ms ease, transform 120ms ease, box-shadow 120ms ease;
}

.btn-view-project:hover{
  background-color: #e14d06; 
  border-color: #e14d06;
  color: #fff;
}

.btn-view-project:active{
  background-color: #c74305; 
  border-color: #c74305;
}

.btn-view-project:focus-visible{
  outline: 2px solid #fb5607;
  outline-offset: 2px;
}

.project-img-wrapper {
  width: 100%;
  height: 120px; 
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #f8f9fa;
}
.project-img {
  max-width: 100%;
  max-height: 100%;
  object-fit: contain; 
}

.card-title {
  font-size: 1rem;
  margin-bottom: 0.5rem;
}
.card-text {
  color: #555;
}
</style>

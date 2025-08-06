<template>
  <div class="col-12 col-lg-4 d-flex">
    <div class="card flex-fill p-3 m-2 bg-dark text-white">
      <img
        :src="project.image"
        class="card-img-top"
        alt="Project Image"
        style="max-height: 200px; object-fit: contain;"
      />
      <div class="card-body">
        <h3 class="card-title">{{ project.title }}</h3>
        <p class="card-text">{{ project.description }}</p>
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

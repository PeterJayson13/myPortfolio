<template>
  <section id="projects" class="mt-5">
    <div class="container-fluid">
      <h1 class="text-center mt-5 p-5 project-title">My <span class="highlight">Projects</span></h1>
      <div class="row text-center px-4 g-4 justify-content-center">
        <ProjectCard
          v-for="(project, index) in projects"
          :key="index"
          :project="project"
        />
      </div>
    </div>
  </section>
</template>

<script setup>
import projects from '../data/project.js';
import ProjectCard from './ProjectCard.vue';
</script>

<style>
.project-title {
  font-family: 'Archivo Black', sans-serif;
  color: #fb5607;
}
.highlight {
  color: black;
  font-family: 'Archivo Black', sans-serif;
}

</style>
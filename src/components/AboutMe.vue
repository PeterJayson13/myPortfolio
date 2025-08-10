<template>
  <section class="about-section bg-dark">
    <div class="container text-white">
      <h1 class="about-title">About <span class="highlight">Me</span></h1>
      <div class="about-columns">
        <p>
          Hi, I’m Peter — a web developer passionate about creating clean, responsive, and user-friendly websites using Vue.js and the MERN stack. I enjoy transforming ideas into functional, visually appealing applications that work smoothly and look great.
        </p>
        <p>
          Before becoming a developer, I worked in the BPO industry as a technical support representative for 5 years. This experience strengthened my problem-solving skills, attention to detail, and ability to remain calm under pressure — qualities I now apply in web development.
        </p>
        <p>
          When I’m not coding, I love reading manga, watching Netflix, and playing games like Counter-Strike and Valorant. I’m always open to new projects and opportunities to grow.
        </p>
      </div>
    </div>
  </section>
</template>

<script setup>
// About Me section — easy to edit content and styling
</script>

<style scoped>
.about-section {
  margin-top: 80px; /* space from landing section */
  padding: 80px 20px; /* more space from landing section */
}

.about-title {
  font-size: 2rem;
  margin-bottom: 2rem;
  font-family: 'Archivo Black', sans-serif;
  text-align: center;
}

.highlight {
  color: #fb5607;
  font-family: 'Archivo Black', sans-serif;
}

.about-columns {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  column-gap: 150px; /* increased gap between columns */
  row-gap: 150px; /* increased gap between rows */
  text-align: left; /* paragraphs aligned left */
  max-width: 1500px;
  margin: 0 auto;
}

.about-columns p {
  line-height: 1.7;
  margin: 0;
}

@media (max-width: 768px) {
  .about-columns {
    grid-template-columns: 1fr;
  }
}
</style>

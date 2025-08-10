<template>
  <section id="landing" class="landing-section">
    <div class="container">
      <div class="row align-items-center text-center text-md-start g-4">
        <!-- Keep photo on the left -->
        <div class="col-md-6 text-center">
          <img
            src="/images/ProfilePic1.jpg"
            id="profilepic"
            class="img-fluid shadow"
            alt="Peter Jayson Bongabong"
            loading="lazy"
            decoding="async"
            sizes="(max-width: 768px) 70vw, 250px"
          />
        </div>
        <!-- Text on the right -->
        <div class="col-md-6 px-3">
          <h1 class="archivo-black name-heading">Peter Jayson Bongabong</h1>
          <h3 class="archivo-black web">Web Developer</h3>
          <p class="lead mt-3">
            Hi there, I'm Peter — a Web Developer who loves building clean and creative websites. I'm just getting started, but I'm all in.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.web {
  color: #fb5607;
}
#profilepic {
  width: 250px;
  height: 250px;
  object-fit: cover;
  object-position: top;
  border-radius: 50%;
  border: 4px solid #fb5607;
  margin-top: 20px;
}
.archivo-black {
  font-family: "Archivo Black", sans-serif;
}
.name-heading {
  font-size: clamp(1.8rem, 3vw, 2.5rem);
}
.web {
  font-size: clamp(1.2rem, 2.5vw, 1.6rem);
}
.landing-section {
  padding-top: 60px; /* space from sticky navbar */
}
</style>

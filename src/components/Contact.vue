<template>
  <section id="contacts" class="contact-section py-5">
    <div class="container">
      <div class="row text-center mb-4">
        <div class="col-12">
          <h1 class="contact-title">Let’s <span class="accent">Connect</span></h1>
        </div>
      </div>

      <div class="row gy-4 align-items-stretch text-center text-md-start">
        <!-- Map -->
        <div class="col-md-6">
          <iframe
            src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d123504.1482937747!2d120.9345330389333!3d14.685934005162424!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x3397b41dae605e5b%3A0x4258953c2333ea6a!2sCaloocan%2C%20Metro%20Manila!5e0!3m2!1sen!2sph!4v1722215160866!5m2!1sen!2sph"
            class="map-frame w-100 rounded-4"
            height="420"
            allowfullscreen
            loading="lazy"
            referrerpolicy="no-referrer-when-downgrade">
          </iframe>
        </div>

        <!-- Form -->
        <div class="col-md-6" id="form-col">
          <form @submit.prevent="submitForm" class="submitForm p-4 p-md-5 rounded-4">
            <div class="mb-3">
              <label for="name" class="form-label">Name</label>
              <input type="text" v-model="name" class="form-control" id="name" placeholder="Your name" required>
            </div>

            <div class="mb-3">
              <label for="email" class="form-label">Email address</label>
              <input type="email" v-model="email" class="form-control" id="email" placeholder="name@example.com" required>
            </div>

            <div class="mb-4">
              <label for="message" class="form-label">Message</label>
              <textarea v-model="message" class="form-control" id="message" rows="5" placeholder="How can I help?" required></textarea>
            </div>

            <div class="d-flex flex-wrap align-items-center justify-content-between gap-3">
              <!-- Socials -->
              <div class="d-flex align-items-center gap-3">
                <a href="https://github.com/PeterJayson13" target="_blank" aria-label="GitHub" title="GitHub">
                  <img src="/images/Github.png" class="img-fluid social-icon" alt="GitHub">
                </a>
                <a href="https://gitlab.com/peterbongabong7" target="_blank" aria-label="GitLab" title="GitLab">
                  <img src="/images/Gitlab.png" class="img-fluid social-icon" alt="GitLab">
                </a>
                <a href="https://www.linkedin.com/in/peter-jayson-bongabong-b43793365/" target="_blank" aria-label="LinkedIn" title="LinkedIn">
                  <img src="/images/Linkedin.png" class="img-fluid social-icon" alt="LinkedIn">
                </a>
              </div>

              <!-- Actions -->
              <div class="ms-md-auto">
                <button
                  type="submit"
                  class="btn btn-custom"
                  data-bs-toggle="modal"
                  data-bs-target="#myModal"
                  :disabled="isLoading">
                  {{ isLoading ? "Sending..." : "Submit" }}
                </button>

                <div class="d-flex justify-content-end mt-2">
                  <div ref="recaptchaContainer"></div>
                </div>
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
    import { ref, onMounted, onBeforeUnmount } from 'vue';
    import { Notyf } from 'notyf';
    import 'notyf/notyf.min.css';

    const notyf = new Notyf();
    const WEB3FORMS_ACCESS_KEY = "31457fb4-8955-4f56-9efd-7684210a1b64";

    const subject = "New message from portfolio contact form";

    const name = ref("");
    const email = ref("");
    const message = ref("");

    const isLoading = ref(false);

    const submitForm = async () => {
        // Set the loading state to true.
        if ( !recaptchaToken.value){
            notyf.error('Please verify that you are not a robot.');
            return;
        }
        isLoading.value = true;
        try{

    const response = await fetch("https://api.web3forms.com/submit", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    Accept: "application/json",
                },
                body: JSON.stringify({
                    access_key: WEB3FORMS_ACCESS_KEY,
                    subject: subject,
                    name: name.value,
                    email: email.value,
                    message: message.value,
                }),
            });
            const result = await response.json();
            if (result.success) {
                console.log(result);
                // Set the loading state to false.
                isLoading.value = false;
                notyf.success("Message Sent!");
                }
            } catch (error) {
                    console.log(error);
                    isLoading.value = false;
                    notyf.error("Failed to send message.");
                } finally {
                    resetRecaptcha();
                }
            }

    const SITE_KEY = '6LfEy5IrAAAAAPzOSH2nFHSSAl2q5Ufj2uwh381U';  // Replace with your site key

    const recaptchaContainer = ref(null);
    const recaptchaWidgetId = ref(null);
    const recaptchaToken = ref('');

    // Callback called by reCAPTCHA when successful
    function onRecaptchaSuccess(token) {
      recaptchaToken.value = token;
    }

    // Callback when expired
    function onRecaptchaExpired() {
      recaptchaToken.value = '';
    }

    // Function to render the reCAPTCHA widget
    function renderRecaptcha() {
      if (!window.grecaptcha) {
        console.error('reCAPTCHA not loaded');
        return;
      }

      recaptchaWidgetId.value = window.grecaptcha.render(recaptchaContainer.value, {
        sitekey: SITE_KEY,
        size: 'normal', // or 'compact'
        callback: onRecaptchaSuccess,
        'expired-callback': onRecaptchaExpired,
      });
    }

    // Function to reset reCAPTCHA 
    function resetRecaptcha() {
      if (recaptchaWidgetId.value !== null) {
        window.grecaptcha.reset(recaptchaWidgetId.value);
        recaptchaToken.value = '';
      }
    }

    onMounted(() => {

    const interval = setInterval(() => {
        if (window.grecaptcha && window.grecaptcha.render) {
          renderRecaptcha();
          clearInterval(interval);
        }
      }, 100);

      onBeforeUnmount(() => {
        clearInterval(interval);
      });
    });


</script>

<style scoped>
.contact-section { 
  scroll-margin-top: 80px; 
}
.contact-title { 
  font-family: 'Archivo Black', sans-serif; 
  margin: 0; 
}
.accent { 
  color: #fb5607; 
}
.map-frame { 
  border: 0; 
  box-shadow: 0 8px 24px rgba(0,0,0,0.08); 
}
.submitForm{
  background-color: #ffffff;
  color: #1f2937;
  border: 1px solid #e5e7eb;
  box-shadow: 0 10px 30px rgba(0,0,0,0.06);
}

.form-label { 
  font-weight: 600; 
}
.form-control{
  background: #fff;
  color: #111;
  border: 1px solid #dfe3e8;
  border-radius: 10px;
  padding: 10px 12px;
  transition: border-color 120ms ease, box-shadow 120ms ease;
}
.form-control:focus{
  border-color: #fb5607;
  box-shadow: 0 0 0 0.2rem rgba(251, 86, 7, 0.15);
}

.social-icon { 
  height: 36px; 
  opacity: 0.9; 
  transition: transform 120ms ease, opacity 120ms ease; 
}
.social-icon:hover { 
  transform: translateY(-2px); 
  opacity: 1; 
}
.btn-custom{
  background-color: #fb5607;
  color: #fff;
  border: 1px solid #fb5607;
  border-radius: 10px;
  padding: 10px 14px;
  transition: background-color 150ms ease, border-color 150ms ease, transform 120ms ease;
}
.btn-custom:hover {
  background-color: #e14d06;
  border-color: #e14d06;
}
.btn-custom:active { 
  background-color: #c74305; 
  border-color: 
  #c74305; 
}
.btn-custom:focus-visible { 
  outline: 2px solid #fb5607; 
  outline-offset: 2px; 
}
</style>
<template>
  <!-- Container  -->
  <div class="container">
    <!-- Header  -->
    <header class="header">
      <div class="header-img">
        <img :src="headerImage" alt="Header Image" />
      </div>
      <div class="header-layer"></div>
    </header>

    <!-- Landing  -->
    <div class="landing">
      <!-- Heading  -->
      <h1 class="heading">Isfhan Ahmed</h1>
      <!-- Sub heading  -->
      <h1 class="sub-heading">solving problems using technology</h1>
      <!-- Text  -->
      <p class="text">
        I'm a Full Stack Developer . I mostly use PHP , JavaScript , Laravel ,
        Python, and lot of other framework and library related to these
        technologies .
      </p>
      <!-- Button -->
      <div class="button">
        <button
          @click="showFormModal = !showFormModal"
          class="action-btn"
          role="button"
        >
          contact me
        </button>
        <button
          @click="showAboutModal = !showAboutModal"
          class="action-btn about-btn"
          role="button"
        >
          about me
        </button>
      </div>
      <ul class="icons">
        <li>
          <a target="blank" href="https://www.facebook.com/isfhan.ahmed1"
            ><img :src="facebookIcon" alt=""
          /></a>
        </li>
        <li>
          <a target="blank" href="https://www.linkedin.com/in/isfhan/"
            ><img :src="linkedinIcon" alt=""
          /></a>
        </li>
        <li>
          <a target="blank" href="https://github.com/Isfhan"
            ><img :src="githubIcon" alt=""
          /></a>
        </li>
      </ul>
    </div>

    <!-- Modals  -->
    <div v-if="showFormModal" class="modal">
      <!-- Wrapper  -->
      <div @click="closeModal" class="wrapper">
        <!-- Form  -->
        <form class="form">
          <!-- Heading  -->
          <div class="heading"><h1>contact form</h1></div>
          <!-- Form control  -->
          <div class="form-control">
            <input
              required
              type="text"
              v-model="name"
              placeholder="Your Name"
            />
          </div>
          <!-- Form control  -->
          <div class="form-control">
            <input
              type="email"
              required
              v-model="email"
              placeholder="Your Email"
            />
          </div>
          <!-- Form control  -->
          <div class="form-control">
            <textarea
              placeholder="Message"
              v-model="message"
              cols="30"
              rows="10"
              required
            ></textarea>
          </div>
          <!-- Form control  -->
          <div class="form-control">
            <button @click.prevent="submit" type="submit" class="submit">
              submit
            </button>
          </div>
        </form>
      </div>
    </div>

    <div v-if="showNotificationModal" class="modal">
      <div class="wrapper">
        <div class="content">
          <img width="80px" :src="checkIcon" alt="Check icon" />
          <h1>Thank you</h1>
          <p class="message">the form was submitted successfully</p>
          <button
            class="action-btn"
            @click="
              showNotificationModal = !showNotificationModal;
              showFormModal = !showFormModal;
            "
          >
            close
          </button>
        </div>
      </div>
    </div>

    <div v-if="showloadingModal" class="modal">
      <div class="wrapper">
        <div class="lds-ring">
          <div></div>
          <div></div>
          <div></div>
          <div></div>
        </div>
      </div>
    </div>

    <div v-if="showAboutModal" class="modal">
      <div @click="closeAboutModal" class="wrapper">
        <div class="content">
          <h1 class="heading">about me</h1>
          <p class="text">
            I am a full-stack developer. I mainly use PHP, JavaScript, Laravel,
            Python and many other frameworks and libraries related to these
            technologies. I have a love for Machine Learning, Data Science and
            Artificial Intelligence. I am also learning Artificial Intelligence
            from UIT. I love Computer Vision and want to be a part of Computer
            Vision industry in future. I am currently working on Shopware plugin
            development and other backend tasks, but I can also work on the
            front-end. I love developing projects from scratch. I have worked a
            lot with PHP and JavaScript. Besides front-end and back-end
            programming, I am also passionate about giving talks and sharing my
            knowledge. I have a YouTube channel where I post videos about
            developer life.
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
// Importing things we need
import headerImage from "../assets/Navimg.svg";
import facebookIcon from "../assets/facebook.svg";
import linkedinIcon from "../assets/linkedin.svg";
import githubIcon from "../assets/github.svg";
import checkIcon from "../assets/check.svg";
import { ref } from "vue";

// Varaibles
const name = ref("");
const email = ref("");
const message = ref("");
const showFormModal = ref(false);
const showNotificationModal = ref(false);
const showloadingModal = ref(false);
const showAboutModal = ref(false);

// Functions
const submit = async () => {
  if (name.value === "" || email.value === "" || message.value === "") return;
  showloadingModal.value = !showloadingModal.value;
  // Making f etch request
  const response = await fetch(
    "https://formsubmit.co/ajax/isfhan729@gmail.com",
    {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
        Accept: "application/json",
      },
      body: JSON.stringify({
        name: name.value,
        email: email.value,
        message: message.value,
      }),
    }
  );
  // Parsing data
  const data = await response.json();
  // Checking if request is success
  if (data.success == "true") {
    showNotificationModal.value = !showNotificationModal.value;
    showloadingModal.value = !showloadingModal.value;
  } else {
    showloadingModal.value = !showloadingModal.value;
  }
};

const closeModal = (e) => {
  if (!e.target.classList.contains("wrapper")) return;
  showFormModal.value = !showFormModal.value;
};
const closeAboutModal = (e) => {
  if (!e.target.classList.contains("wrapper")) return;
  showAboutModal.value = !showAboutModal.value;
};
</script>

<style >


* {
  padding: 0;
  margin: 0;
  font-family: "Outfit", sans-serif;
}

body {
  min-height: 100vh;
  background: #fff;
}

.header {
  position: relative;
  background: url("~assets/isfhan.jpg");
  background-size: cover;
  background-repeat: no-repeat;
  background-position-y: -300px;
}

.header-layer {
  position: absolute;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  background: #6b0604d1;
}

.header-img {
  display: grid;
  place-items: center;
  position: relative;
  position: relative;
  z-index: 2;
}
.header-img > img {
  position: relative;
  top: 50px;
}

.landing {
  max-width: 1440px;
  margin: auto;
  margin-top: 80px;
  text-align: center;
  padding: 10px;
}

.landing > .heading {
  font-size: 3rem;
  font-family: "Outfit", sans-serif;
  text-transform: capitalize;
  color: #222;
}
.landing > .sub-heading {
  font-size: 1.5rem;
  text-transform: capitalize;
  color: #fff;
  text-transform: capitalize;
  background: #6b0504;
  display: inline-block;
  padding: 10px 20px;
  margin: 10px 0px;
  font-weight: 400;
  border-radius: 3px;
}
.landing > .text {
  font-size: 20px;
  padding: 20px 0px;
  font-weight: 200;
  line-height: 1.9rem;
  letter-spacing: 1px;
  max-width: 450px;
  margin: auto;
}

.landing > .button > .action-btn {
  font-size: 20px;
  text-transform: capitalize;
  font-weight: 400;
  position: relative;
  overflow: hidden;
  border: 2px solid #6b0504;
  color: #6b0504;
  text-decoration: none;
  cursor: pointer;
  background: transparent;
  padding: 10px 20px;
  transition: 0.3s linear;
  min-width: 150px;
}
.landing > .button > .about-btn {
  background: #6b0504;
  color: #fff;
  min-width: 150px;
  margin-left: 10px;
}

.landing > .button > .action-btn:hover {
  background: #6b0504;
  color: #fff;
}
.icons {
  display: flex;
  list-style: none;
  justify-content: center;
  gap: 20px;
  margin-top: 80px;
}

.icons > li > a > img {
  width: 30px;
}

.modal {
  position: relative;
}

.modal > .wrapper {
  background: rgba(34, 34, 34, 0.637);
  position: fixed;
  width: 100%;
  height: 100%;
  top: 0;
  left: 0;
  display: grid;
  place-items: center;
  z-index: 3;
}

.modal > .wrapper .form {
  display: flex;
  flex-direction: column;
  gap: 20px;
  background: #fff;
  padding: 20px;
  border-radius: 5px;
}

.modal > .wrapper .form > .heading {
  font-size: 1.5rem;
  font-family: "Outfit", sans-serif;
  text-transform: capitalize;
  color: #222;
  text-align: center;
}

.modal > .wrapper .form > .form-control > input {
  width: 100%;
  padding: 10px 0px;
  text-indent: 10px;
  border: 1px solid #2222;
  border-radius: 5px;
  min-width: 400px;
  font-size: 20px;
}
.modal > .wrapper .form > .form-control > textarea {
  width: 100%;
  padding: 10px 0px;
  text-indent: 10px;
  border: 1px solid #2222;
  border-radius: 5px;
  min-width: 400px;
  font-size: 20px;
}
.modal > .wrapper .form > .form-control > .submit {
  width: 100%;
  font-size: 20px;
  text-transform: uppercase;
  font-weight: 400;
  cursor: pointer;
  border-radius: 3px;
  background: transparent;
  background: transparent;
  color: #fff;
  transition: 0.3s ease;
  border: 2px solid #6b0504;
  background: #6b0504;
  padding: 10px;
}

.modal > .wrapper > .content {
  background: #fff;
  padding: 20px;
  border-radius: 5px;
  text-align: center;
  max-width: 500px;
}

.modal > .wrapper > .content > .text {
  font-size: 20px;
  padding: 20px 0px;
  font-weight: 200;
  line-height: 1.9rem;
  letter-spacing: 1px;
}
.modal > .wrapper > .content > .heading {
  display: flex;
  flex-direction: column;
  gap: 20px;
  background: #fff;
  padding: 20px;
  border-radius: 5px;
  text-transform: capitalize;
}

.modal > .wrapper > .content > .message {
  padding: 10px 0px;
  text-transform: capitalize;
}

.modal > .wrapper > .content > .action-btn {
  font-size: 20px;
  text-transform: capitalize;
  font-weight: 400;
  position: relative;
  overflow: hidden;
  border: 2px solid #6b0504;
  color: #6b0504;
  text-decoration: none;
  cursor: pointer;
  background: transparent;
  padding: 10px 20px;
  transition: 0.3s linear;
  border-radius: 5px;
  margin-top: 10px;
}

.lds-ring {
  display: inline-block;
  position: relative;
  width: 80px;
  height: 80px;
}
.lds-ring div {
  box-sizing: border-box;
  display: block;
  position: absolute;
  width: 64px;
  height: 64px;
  margin: 8px;
  border: 8px solid #fff;
  border-radius: 50%;
  animation: lds-ring 1.2s cubic-bezier(0.5, 0, 0.5, 1) infinite;
  border-color: #fff transparent transparent transparent;
}
.lds-ring div:nth-child(1) {
  animation-delay: -0.45s;
}
.lds-ring div:nth-child(2) {
  animation-delay: -0.3s;
}
.lds-ring div:nth-child(3) {
  animation-delay: -0.15s;
}
@keyframes lds-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>
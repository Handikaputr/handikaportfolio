<template>
  <section id="home" class="w-full overflow-y-hidden h-[720px] flex flex-wrap justify-center overflow-x-hidden relative">
    <div class="box w-full max-w-7xl flex animed flex-wrap overflow-y-hidden overflow-x-hidden">
      <div class="picture-content w-full items-end md:w-1/2 flex md:items-center justify-center">
        <div ref="cardsContainer" class="picture-content scale-90 md:scale-100 w-60 h-96 flex items-center justify-center relative">
          <div class="card card-img card-back-img absolute w-60 h-96 rounded-xl border border-white overflow-hidden">
            <img class="object-cover w-full h-full" :src="'assetImg/namecard.webp'" alt="">
          </div>
          <div class="card absolute w-60 h-96 rounded-xl overflow-hidden border border-white">
            <img class="object-cover w-full h-full" :src="'assetImg/Handikaputra.webp'" alt="">
          </div>
          <img class="absolute animate__animated animate__zoomIn animate__faster -bottom-20 -left-32 scale-75" :src="'/assetImg/1x/moon.webp'" alt="">
          <img class="absolute -bottom-11 -left-12" :src="'/assetImg/1x/cloud2.webp'" alt="">
          <dotlottie-player class="absolute animate__animated animate__fadeInUp -left-24 animate__delay-1s mt-20 w-36 h-36"
            src="https://lottie.host/1622d024-45a7-4f11-bdde-f24498da63be/ojGF2Ujsfj.json" background="transparent" speed="1" loop autoplay>
          </dotlottie-player>
          <img class="absolute animate__animated animate__zoomIn -bottom-14 left-8" :src="'/assetImg/1x/cloud1.webp'" alt="">
          <img class="absolute animate__animated animate__zoomIn -bottom-12 -left-24 scale-125" :src="'/assetImg/1x/cloud4.webp'" alt="">
          <img class="absolute animate__animated animate__zoomIn -bottom-16 -left-24" :src="'/assetImg/1x/cloud3.webp'" alt="">
        </div>
      </div>
      <div class="text-content mt-1 md:mt-0 flex px-8 items-center justify-center w-full md:w-1/2 p-3">
        <div class="box w-full h-fit flex gap-2 justify-center relative items-center">
          <div class="text h-full flex-1 max-w-full">
            <div class="name text-4xl mb-2 animate__animated animate__slowest animate__lightSpeedInRight kanit text-gradient">
              Handika Putra
            </div>
            <div class="text-2xl text-elipsis animate__animated animate__slow animate__lightSpeedInRight flex gap-2">
              I'am
              <div class="job-container px-4 min-w-fit whitespace-nowrap box-content overflow-hidden relative bg-purple-500 w-fit text-white">
                <div class="job-animation w-fit">{{ jobText }}</div>
              </div>
              Developer
            </div>
            <div class="text-sm animate__animated animate__lightSpeedInRight animate__delay-1s border-t-2 mt-4 pt-2 border-purple-600">
              Explore my portfolio to see a showcase of my work, from interactive 2D experiences in Unity to robust APIs and dynamic websites. Whether you're looking for a talented developer to bring your vision to life or simply want to learn more about my journey, you've come to the right place.
            </div>
            <div class="flex animate__animated animate__lightSpeedInRight animate__delay-1s">
<a :href="'/cv3.pdf'" download
              class="flex group  items-center gap-2 bg-gradient-to-br from-purple-400 to-blue-600 rounded-full pl-4 mt-2 hover:bg-purple-400 hover:text-white duration-200 w-fit">
              Download CV
              <div class="w-10 h-10 bg-white border group-hover:bg-black border-purple-500 shadow-sm flex items-center justify-center pl-1 rounded-full">
                <ion-icon class="text-2xl" name="download"></ion-icon>
              </div>
            </a>
            <a href="https://www.linkedin.com/in/handika-putra-478642312/" class="text-blue-400 w-10  h-10 flex items-center justify-center rounded-full  hover:text-blue-600 duration-200 ml-4 mt-2 animate__animated animate__pulse animate__infinite" target="_blank" rel="noopener noreferrer">
              <ion-icon class="text-xl w-10 h-10" name="logo-linkedin"></ion-icon>
            </a>
            </div>
            
          </div>
        </div>
      </div>
    </div>
    <img :src="'/assetImg/cloud/1x/blueCloud.webp'" class="left-0 -bottom-2 absolute w-screen -z-10" alt="">
  </section>
</template>
<!-- end template -->
<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const cardsContainer = ref(null)
let cards = []
let intervalId = null
const INTERVAL_MS = 10000

function shufCard() {
  cards.forEach((card) => card.classList.toggle('card-back-img'))
}

function startInterval() {
  if (intervalId) clearInterval(intervalId)
  intervalId = setInterval(shufCard, INTERVAL_MS)
}

function cardClickHandler() {
  shufCard()
  startInterval()
}

// Typing animation logic (Vue version)
const jobText = ref('')
const jobs = ["Website", "API", "Game"]
let jobIndex = 0
let charIndex = 0
let isDeleting = false
let typingTimeout = null
const typingSpeed = 150
const erasingSpeed = 100
const newWordDelay = 2000

function typeJob() {
  const currentJob = jobs[jobIndex]
  if (!isDeleting && charIndex < currentJob.length) {
    charIndex++
    jobText.value = currentJob.substring(0, charIndex)
    typingTimeout = setTimeout(typeJob, typingSpeed)
  } else if (isDeleting && charIndex > 0) {
    charIndex--
    jobText.value = currentJob.substring(0, charIndex)
    typingTimeout = setTimeout(typeJob, erasingSpeed)
  } else if (!isDeleting && charIndex === currentJob.length) {
    isDeleting = true
    typingTimeout = setTimeout(typeJob, newWordDelay)
  } else if (isDeleting && charIndex === 0) {
    isDeleting = false
    jobIndex = (jobIndex + 1) % jobs.length
    typingTimeout = setTimeout(typeJob, typingSpeed)
  }
}

onMounted(() => {
  if (cardsContainer.value) {
    cards = Array.from(cardsContainer.value.querySelectorAll('.card'))
    cards.forEach((c) => c.addEventListener('click', cardClickHandler))
  }
  startInterval()
  typeJob()
})

onBeforeUnmount(() => {
  if (intervalId) clearInterval(intervalId)
  cards.forEach((c) => c.removeEventListener('click', cardClickHandler))
  if (typingTimeout) clearTimeout(typingTimeout)
})
</script>

<style scoped>
.card {
  transition-duration: 0.5s;
  margin: 0;
  margin-right: 0rem;
  box-shadow: 4px 7px 10px rgba(0, 0, 0, 0.5);
}
.card-back-img {
  z-index: -1;
  margin-left: 6rem;
  margin-top: 1rem;
  rotate: 15deg;
  animation-delay: 0.5s;
  scale: 0.9;
}
section {
  height: 100vh;
  min-height: 700px;
  max-height: 800px;
  overflow-y: hidden;
}
.job-animation {
  animation: job 10s infinite;
  animation-timing-function: cubic-bezier(0.25, 0.1, 0.25, 1);
}
</style>

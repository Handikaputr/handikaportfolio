<script setup>
import { ref, onMounted, onUnmounted, computed } from 'vue'

const lastSlide = ref(0)
const currentSlide = ref(0)
const isAutoPlaying = ref(true)
const carouselTrack = ref(null)
let autoPlayInterval = null

const projects = [
  {
    id: 1,
    title: 'HAWI REGENCY',
    description: 'Unity Game Project, edugame untuk bptik (magang)',
    image: 'assetImg/hawi.png',
    videoUrl: 'https://www.youtube.com/embed/K4ccnudcaQU?si=vqOECffCh65oS1ri',
    playUrl: 'https://dev.teknoreka.com/edugame/Hawi%20Regency/',
    category: 'Unity Game',
    gradient: 'from-purple-500 to-pink-600'
  },
  {
    id: 2,
    title: 'MOLEKUL KIMIA',
    description: 'Unity Game Project, edugame untuk brite (magang)',
    image: 'assetImg/Cuplikan layar 2025-05-06 201814.png',
    videoUrl: 'https://www.youtube-nocookie.com/embed/7Y9Xu__r3WA?si=dIniBAmT-rNFl3yw',
    playUrl: 'https://dev.teknoreka.com/edugame/Jelajah%20Molekul%20Kimia%20/',
    category: 'Educational Game',
    gradient: 'from-blue-500 to-cyan-600'
  },
  {
    id: 3,
    title: 'JELAJAH INDONESIA',
    description: 'Unity Game Project, edugame untuk brite (magang)',
    image: 'assetImg/Cuplikan layar 2025-05-06 202849.png',
    videoUrl: 'https://www.youtube-nocookie.com/embed/iW6Oeo4hS4Q?si=ugskNZiQ-LpgQeDN',
    playUrl: 'https://dev.teknoreka.com/edugame/Jelajah%20Indonesia/',
    category: 'Cultural Game',
    gradient: 'from-green-500 to-emerald-600'
  },
  {
    id: 4,
    title: 'SI JALI',
    description: 'Unity Game Project, edugame untuk brite (magang)',
    image: 'assetImg/Cuplikan layar 2025-05-06 202657.png',
    videoUrl: 'https://www.youtube.com/embed/_Qah22FFpIQ?si=UjLO_OZyAbHa5tGN',
    playUrl: 'https://dev.teknoreka.com/edugame/Perjalanan%20Si%20Jali/',
    category: 'Adventure Game',
    gradient: 'from-orange-500 to-red-600'
  }
]

const totalSlides = projects.length
const slidesPerView = computed(() => {
  if (typeof window === 'undefined') return 1
  if (window.innerWidth >= 1280) return 3
  if (window.innerWidth >= 768) return 2
  return 1
})
const maxSlide = computed(() => Math.max(0, totalSlides - slidesPerView.value))

// Navigation
const nextSlide = () => { 
  lastSlide.value = currentSlide.value;
  currentSlide.value = currentSlide.value >= maxSlide.value ? 0 : currentSlide.value + 1 

}
const prevSlide = () => { 
  lastSlide.value = currentSlide.value;
  currentSlide.value = currentSlide.value <= 0 ? maxSlide.value : currentSlide.value - 1 
}
const goToSlide = (i) => { currentSlide.value = Math.min(i, maxSlide.value) }

const project = computed(() => projects[currentSlide.value])
// Modal video
const showVideo = (url) => {
  const modal = document.createElement('div')
  modal.className = 'fixed inset-0 bg-black bg-opacity-75 flex items-center justify-center z-50 p-4'
  modal.innerHTML = `
    <div class="relative max-w-4xl w-full">
      <button class="absolute -top-12 right-0 text-white text-2xl hover:text-gray-300 transition-colors">&times;</button>
      <div class="relative pb-[56.25%] h-0">
        <iframe src="${url}" class="absolute top-0 left-0 w-full h-full rounded-lg" frameborder="0" allowfullscreen></iframe>
      </div>
    </div>
  `
  document.body.appendChild(modal)
  modal.addEventListener('click', (e) => {
    if (e.target === modal || e.target.textContent === '×') document.body.removeChild(modal)
  })
}

// Autoplay
const startAutoPlay = () => { stopAutoPlay(); isAutoPlaying.value = true; autoPlayInterval = setInterval(nextSlide, 10000) }
const stopAutoPlay = () => { isAutoPlaying.value = false; if (autoPlayInterval) { clearInterval(autoPlayInterval); autoPlayInterval = null } }

// Touch swipe

const handleResize = () => { if (currentSlide.value > maxSlide.value) currentSlide.value = maxSlide.value }

onMounted(() => { startAutoPlay(); window.addEventListener('resize', handleResize) })
onUnmounted(() => { stopAutoPlay(); window.removeEventListener('resize', handleResize) })
</script>

<template>
  <section id="project" class="w-full min-h-[820px] bg-white flex flex-col items-center justify-center py-20 bg-gradient-to-b from-white to-gray-100 relative overflow-hidden">
    <!-- Header -->
<div class="text-center mb-16 relative z-10 px-4">
  <!-- Animated background decoration -->
  <div class="absolute inset-0 -z-10 opacity-30">
    <div class="absolute top-8 left-1/4 w-32 h-32 bg-gradient-to-br from-blue-200 to-purple-200 rounded-full blur-2xl animate-pulse"></div>
    <div class="absolute -top-4 right-1/3 w-24 h-24 bg-gradient-to-br from-purple-200 to-pink-200 rounded-full blur-xl animate-pulse delay-1000"></div>
  </div>
  
  <div class="relative">
    <h2 class="text-4xl md:text-5xl lg:text-6xl font-bold bg-gradient-to-r from-gray-800 via-gray-700 to-gray-800 bg-clip-text text-transparent font-space tracking-tight">
      My Projects
    </h2>
    <!-- Elegant underline -->
    <div class="w-16 h-0.5 bg-gradient-to-r from-transparent via-gray-400 to-transparent mx-auto mt-3"></div>
  </div>
  
  <p class="text-lg md:text-xl text-gray-600 max-w-2xl mx-auto mt-6 leading-relaxed">
    Explore my collection of 
    <span class="font-semibold text-gray-700 bg-gradient-to-r from-blue-600 to-purple-600 bg-clip-text text-transparent">Unity educational games</span> 
    and interactive projects
  </p>
  
  <!-- Subtle indicators -->
  <div class="flex justify-center items-center gap-6 mt-8 text-sm text-gray-500">
    <div class="flex items-center gap-2">
      <div class="w-1.5 h-1.5 bg-blue-400 rounded-full animate-pulse"></div>
      <span>Educational</span>
    </div>
    <div class="flex items-center gap-2">
      <div class="w-1.5 h-1.5 bg-purple-400 rounded-full animate-pulse delay-300"></div>
      <span>Interactive</span>
    </div>
    <div class="flex items-center gap-2">
      <div class="w-1.5 h-1.5 bg-pink-400 rounded-full animate-pulse delay-700"></div>
      <span>Unity Engine</span>
    </div>
  </div>
</div>

    <!-- Mobile/Tablet: Carousel -->
    <div class="w-full max-w-7xl mx-auto px-4 relative lg:hidden">
      <transition 
        :name="lastSlide == 0 && currentSlide == 3 || lastSlide == 3 && currentSlide == 0  || lastSlide > currentSlide ? 'fader-slide' : 'fade-slide'"
        mode="out-in"
        >
      <div class="relative flex justify-center"
            :key="project.id"
           @mouseenter="stopAutoPlay" @mouseleave="startAutoPlay">
        <div class="flex transition-transform duration-500 ease-in-out"
             ref="carouselTrack">
          <div  class="">
            <div class="group bg-gradient-to-b from-gray-100 to-white rounded-2xl shadow-lg hover:shadow-2xl transition-all duration-300 overflow-hidden h-full flex flex-col border border-gray-100 hover:border-gray-200">
              <div class="relative overflow-hidden">
                <img :src="project.image" :alt="project.title" class="w-full h-48 md:h-56 object-cover transition-transform duration-300 group-hover:scale-105">
                <div class="absolute top-4 left-4">
                  <span :class="`inline-flex items-center px-3 py-1.5 rounded-full text-xs font-semibold bg-gradient-to-r ${project.gradient} text-white shadow-lg`">
                    {{ project.category }}
                  </span>
                </div>
              </div>
              <div class="p-6 flex-1 flex flex-col">
                <h3 class="font-space font-bold text-xl text-gray-800 mb-3 text-center tracking-wide">{{ project.title }}</h3>
                <p class="text-gray-600 text-sm flex-1 leading-relaxed mb-6 text-center">{{ project.description }}</p>
                <div class="space-y-3">
                  <button @click="showVideo(project.videoUrl)" class="w-full h-12 bg-gradient-to-r from-gray-800 to-gray-900 text-white rounded-xl font-medium transition-all duration-300 flex items-center justify-center">▶ View Demo</button>
                  <a :href="project.playUrl" target="_blank" :class="`w-full h-12 bg-gradient-to-r ${project.gradient} text-white rounded-xl font-medium transition-all duration-300 flex items-center justify-center`">🎮 Play Game</a>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
      </transition>
      
      <!-- Arrows -->
      <button @click="prevSlide" class="absolute left-0 top-1/2 -translate-y-1/2 -translate-x-4 w-12 h-12 bg-white rounded-full shadow-lg">‹</button>
      <button @click="nextSlide" class="absolute right-0 top-1/2 -translate-y-1/2 translate-x-4 w-12 h-12 bg-white rounded-full shadow-lg">›</button>
      <!-- Dots -->
      <div class="flex justify-center space-x-3 mt-8">
        <button v-for="n in (maxSlide + 1)" :key="n" @click="goToSlide(n-1)"
                :class="['w-3 h-3 rounded-full border-2', currentSlide === n-1 ? 'bg-gray-800 border-gray-800' : 'border-gray-400']"></button>
      </div>
    </div>

    <!-- Desktop: Static Grid -->
    <div class="hidden lg:grid grid-cols-3 gap-8 w-full max-w-7xl z-10 mx-auto px-4">
      <div v-for="project in projects" :key="project.id" class="group z-10 bg-white rounded-2xl shadow-lg hover:shadow-2xl transition-all duration-300 overflow-hidden flex flex-col border border-gray-100 hover:border-gray-200">
        <div class="relative overflow-hidden">
          <img :src="project.image" :alt="project.title" class="w-full h-56 object-cover transition-transform duration-300 group-hover:scale-105">
          <div class="absolute top-4 left-4">
            <span :class="`inline-flex items-center px-3 py-1.5 rounded-full text-xs font-semibold bg-gradient-to-r ${project.gradient} text-white shadow-lg`">
              {{ project.category }}
            </span>
          </div>
        </div>
        <div class="p-6 flex-1 flex flex-col">
          <h3 class="font-space font-bold text-xl text-gray-800 mb-3 text-center tracking-wide">{{ project.title }}</h3>
          <p class="text-gray-600 text-sm flex-1 leading-relaxed mb-6 text-center">{{ project.description }}</p>
          <div class="space-y-3">
            <button @click="showVideo(project.videoUrl)" class="w-full h-12 bg-gradient-to-r from-gray-800 to-gray-900 text-white rounded-xl font-medium flex items-center justify-center">▶ View Demo</button>
            <a :href="project.playUrl" target="_blank" :class="`w-full h-12 bg-gradient-to-r ${project.gradient} text-white rounded-xl font-medium flex items-center justify-center`">🎮 Play Game</a>
          </div>
        </div>
      </div>
    </div>
     <div class="img absolute -z-1 bottom-0 w-screen">
        <img class="w-full -z-1 " :src="'assetImg/cloud/1x/whiteCloud.webp'" alt="">
    </div>
  </section>
</template>

<style scoped>
.font-space { font-family: 'Space Grotesk', sans-serif; }
.fade-slide-enter-active,
.fade-slide-leave-active {
  transition: all 0.4s ease;
}
.fade-slide-enter-from {
  opacity: 0;
  transform: translateX(60px);
}
.fade-slide-leave-to {
  opacity: 0;
  transform: translateX(-60px);
}

.fader-slide-enter-active,
.fader-slide-leave-active {
  transition: all 0.4s ease;
}
.fader-slide-enter-from {
  opacity: 0;
  transform: translateX(-60px);
}
.fader-slide-leave-to {
  opacity: 0;
  transform: translateX(60px);
}
</style>

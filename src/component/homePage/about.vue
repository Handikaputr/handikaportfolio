<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

const currentSlide = ref(0)
const carouselContainer = ref(null)
const totalSlides = 3
const isAutoPlaying = ref(true)
let autoPlayInterval = 4

const skills = [
  {
    title: 'API Development',
    description: 'I specialize in creating efficient and secure APIs to power various applications. My API development skills include:',
    items: [
      'Designing RESTful APIs',
      'Implementing authentication and authorization',
      'Ensuring data integrity and security',
      'Documenting APIs for easy integration',
      'Optimizing performance and scalability'
    ],
    gradient: 'bg-gradient-to-r from-blue-500 to-purple-600'
  },
  {
    title: 'Web Development',
    description: 'I excel in building responsive and user-friendly websites. My web development skills include:',
    items: [
      'Creating visually appealing and functional websites using HTML, CSS, and JavaScript',
      'Developing robust backend systems with PHP and Laravel',
      'Ensuring cross-browser compatibility and responsive design',
      'Implementing SEO best practices for better visibility'
    ],
    gradient: 'bg-gradient-to-r from-green-500 to-teal-600'
  },
  {
    title: 'Unity Development',
    description: 'I have extensive experience in Unity, where I have developed a range of interactive applications and games.',
    items: [
      'Designing and implementing game mechanics',
      'Creating immersive 2D environments',
      'Integrating animations and physics',
      'Utilizing Unity\'s scripting API for custom functionalities',
      'Optimizing performance for smooth gameplay'
    ],
    gradient: 'bg-gradient-to-r from-orange-500 to-red-600'
  }
]

const nextSlide = () => {
  currentSlide.value = (currentSlide.value + 1) % totalSlides
}

const prevSlide = () => {
  currentSlide.value = (currentSlide.value - 1 + totalSlides) % totalSlides
}

const goToSlide = (index) => {
  currentSlide.value = index
}

const startAutoPlay = () => {
  isAutoPlaying.value = true
  autoPlayInterval = setInterval(nextSlide, 5000)
}

const stopAutoPlay = () => {
  isAutoPlaying.value = false
  if (autoPlayInterval) {
    clearInterval(autoPlayInterval)
    autoPlayInterval = null
  }
}

// Touch/Swipe handling
let startX = 0
let startY = 0
let isDragging = false

const handleTouchStart = (e) => {
  startX = e.touches[0].clientX
  startY = e.touches[0].clientY
  isDragging = true
  stopAutoPlay()
}

const handleTouchMove = (e) => {
  if (!isDragging) return
  e.preventDefault()
}

const handleTouchEnd = (e) => {
  if (!isDragging) return
  
  const endX = e.changedTouches[0].clientX
  const endY = e.changedTouches[0].clientY
  const diffX = startX - endX
  const diffY = startY - endY
  
  // Only trigger swipe if horizontal movement is greater than vertical
  if (Math.abs(diffX) > Math.abs(diffY) && Math.abs(diffX) > 50) {
    if (diffX > 0) {
      nextSlide()
    } else {
      prevSlide()
    }
  }
  
  isDragging = false
  setTimeout(startAutoPlay, 3000) // Resume autoplay after 3 seconds
}

onMounted(() => {
  startAutoPlay()
})

onUnmounted(() => {
  stopAutoPlay()
})
</script>

<template>
  <section id="about" class="w-full flex flex-col justify-center bg-sky-100 items-center overflow-hidden relative min-h-[720px] h-screen py-16">
    <!-- Background cloud -->
    <img :src="'assetImg/cloud/1x/whiteCloud.webp'" class="absolute bottom-0 left-0 w-full z-10 object-cover" alt="">
    
    <div class="container mx-auto px-4 flex flex-col items-center justify-center h-full z-20">
      <!-- Technology Icons -->
      <div class="flex w-full max-w-md gap-8 items-center justify-center mb-8 opacity-70 hover:opacity-90 transition-opacity duration-300">
        <div class="flex-1 flex justify-center transform hover:scale-120 transition-transform duration-300">
          <img class=" h-18  md:h-24 filter drop-shadow-lg" :src="'assetImg/pluginapp/laravel.svg'" alt="Laravel">
        </div>
        <div class="flex-1 flex justify-center transform hover:scale-110 transition-transform duration-300">
          <img class=" h-12  md:h-16 filter drop-shadow-lg" :src="'assetImg/pluginapp/pngegg.png'" alt="Vue.js">
        </div>
        <div class="flex-1 flex justify-center transform hover:scale-110 transition-transform duration-300">
          <img class=" h-12 scale-1/2 md:h-16 filter drop-shadow-lg" :src="'assetImg/pluginapp/Tailwind CSS.svg'" alt="Tailwind CSS">
        </div>
      </div>

      <!-- Header Text -->
      <div class="text-center mb-12 max-w-2xl">
        <h2 class="text-4xl md:text-5xl lg:text-6xl font-bold text-gray-800 mb-4 font-space bg-gradient-to-r from-blue-600 to-purple-600 bg-clip-text text-transparent">
          Specializing In
        </h2>
        <p class="text-base md:text-lg text-gray-600 leading-relaxed px-4">
          I am a passionate and versatile developer with expertise in Unity, API development, and web development
        </p>
      </div>

      <!-- Desktop View: All cards visible -->
      <div class="hidden lg:flex gap-6 max-w-7xl w-full justify-center">
        <div v-for="(skill, index) in skills" :key="index" 
             class="skill-card flex-1 max-w-sm bg-white rounded-2xl shadow-2xl overflow-hidden transform hover:-translate-y-2 transition-all duration-300 hover:shadow-3xl">
          <div :class="skill.gradient" class="h-2"></div>
          <div class="p-6">
            <div :class="skill.gradient" class="text-xl font-bold text-white py-2 px-4 rounded-lg mb-4 w-fit bg-clip-padding">
              {{ skill.title }}
            </div>
            <p class="text-sm text-gray-600 mb-4 leading-relaxed">{{ skill.description }}</p>
            <ul class="space-y-2">
              <li v-for="(item, itemIndex) in skill.items" :key="itemIndex" class="flex items-start">
                <div class="w-2 h-2 rounded-full bg-gradient-to-r from-blue-500 to-purple-600 mt-2 mr-3 flex-shrink-0"></div>
                <span class="text-sm text-gray-700">{{ item }}</span>
              </li>
            </ul>
          </div>
        </div>
      </div>

      <!-- Mobile/Tablet View: Carousel -->
      <div class="lg:hidden w-full max-w-md mx-auto relative">
        <!-- Carousel Container -->
        <div class="relative overflow-hidden rounded-2xl shadow-2xl"
             @touchstart="handleTouchStart"
             @touchmove="handleTouchMove"
             @touchend="handleTouchEnd"
             @mouseenter="stopAutoPlay"
             @mouseleave="startAutoPlay">
          <div class="flex transition-transform duration-500 ease-in-out"
               :style="{ transform: `translateX(-${currentSlide * 100}%)` }"
               ref="carouselContainer">
            <div v-for="(skill, index) in skills" :key="index" 
                 class="w-full flex-shrink-0 bg-white">
              <div :class="skill.gradient" class="h-2"></div>
              <div class="p-6 min-h-[400px]">
                <div :class="skill.gradient" class="text-xl font-bold text-white py-2 px-4 rounded-lg mb-4 w-fit">
                  {{ skill.title }}
                </div>
                <p class="text-sm text-gray-600 mb-4 leading-relaxed">{{ skill.description }}</p>
                <ul class="space-y-2">
                  <li v-for="(item, itemIndex) in skill.items" :key="itemIndex" class="flex items-start">
                    <div class="w-2 h-2 rounded-full bg-gradient-to-r from-blue-500 to-purple-600 mt-2 mr-3 flex-shrink-0"></div>
                    <span class="text-sm text-gray-700">{{ item }}</span>
                  </li>
                </ul>
              </div>
            </div>
          </div>
        </div>

        <!-- Navigation Arrows -->
        <button @click="prevSlide" 
                class="absolute left-2 mt-6 -translate-y-1/2 w-10 h-10 bg-white/90 backdrop-blur-sm rounded-full shadow-lg flex items-center justify-center hover:bg-white hover:scale-110 transition-all duration-200 z-10">
          <svg class="w-5 h-5 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path>
          </svg>
        </button>
        <button @click="nextSlide" 
                class="absolute right-2 mt-6 -translate-y-1/2 w-10 h-10 bg-white/90 backdrop-blur-sm rounded-full shadow-lg flex items-center justify-center hover:bg-white hover:scale-110 transition-all duration-200 z-10">
          <svg class="w-5 h-5 text-gray-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7"></path>
          </svg>
        </button>

        <!-- Dots Indicator -->
        <div class="flex justify-center space-x-2 mt-6">
          <button v-for="(_, index) in skills" :key="index"
                  @click="goToSlide(index)"
                  :class="[
                    'w-3 h-3 rounded-full transition-all duration-300',
                    currentSlide === index 
                      ? 'bg-gradient-to-r from-blue-500 to-purple-600 scale-125' 
                      : 'bg-gray-300 hover:bg-gray-400'
                  ]">
          </button>
        </div>

        
      </div>
    </div>
  </section>
</template>

<style scoped>
.skill-card {
  backdrop-filter: blur(10px);
}

.font-space {
  font-family: 'Space Grotesk', sans-serif;
}

/* Custom scrollbar for webkit browsers */
::-webkit-scrollbar {
  display: none;
}

/* Smooth scrolling */
.scroll-smooth {
  scroll-behavior: smooth;
}

/* Auto-playing indicator animation */
@keyframes pulse {
  0%, 100% { opacity: 1; }
  50% { opacity: 0.5; }
}

.animate-pulse {
  animation: pulse 2s cubic-bezier(0.4, 0, 0.6, 1) infinite;
}

/* Enhanced shadow */
.shadow-3xl {
  box-shadow: 0 35px 60px -12px rgba(0, 0, 0, 0.25);
}
</style>
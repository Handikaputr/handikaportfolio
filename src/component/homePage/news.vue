<template>
  <!-- Achievements Section -->
  <section id="archivement" class="w-full min-h-screen pt-20 relative">

    <!-- Header -->
    <div class="text-center mb-16 relative z-10 px-4">
      <div class="absolute inset-0 -z-10 opacity-20">
        <div
          class="absolute top-8 left-1/3 w-28 h-28 bg-gradient-to-br from-emerald-200 to-teal-200 rounded-full blur-2xl animate-pulse">
        </div>
        <div
          class="absolute -top-4 right-1/4 w-20 h-20 bg-gradient-to-br from-teal-200 to-cyan-200 rounded-full blur-xl animate-pulse delay-1000">
        </div>
      </div>

      <div class="relative">
        <h2
          class="text-4xl md:text-5xl lg:text-6xl font-bold bg-gradient-to-r from-gray-800 via-gray-700 to-gray-800 bg-clip-text text-transparent font-space tracking-tight">
          My Achievements
        </h2>
        <div class="w-16 h-0.5 bg-gradient-to-r from-transparent via-gray-400 to-transparent mx-auto mt-3"></div>
      </div>

      <p class="text-lg md:text-xl text-gray-600 max-w-2xl mx-auto mt-6 leading-relaxed">
        Explore my
        <span
          class="font-semibold text-gray-700 bg-gradient-to-r from-emerald-600 to-teal-600 bg-clip-text text-transparent">milestones</span>
        and recognitions
      </p>
    </div>

    <!-- Content Container -->
    <div class="max-w-7xl mx-auto px-4">
      <!-- Certificates Section -->
      <div class="mb-16">
        <div class="flex items-center justify-between mb-8">
          <h3 class="text-2xl md:text-3xl font-bold text-gray-800">Certificates</h3>
          <button v-if="certificatesData.length > 2" @click="toggleCertificatesExpanded"
            class="flex items-center gap-2 px-4 py-2 bg-gray-100 hover:bg-gray-200 rounded-lg transition-all duration-300">
            <span class="text-gray-600 font-medium">{{ certificatesExpanded ? 'Show Less' : 'Show More' }}</span>
            <svg
              :class="['w-4 h-4 text-gray-600 transition-transform duration-300', certificatesExpanded ? 'rotate-180' : '']"
              fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
            </svg>
          </button>
        </div>

        <!-- Certificates Grid -->
        <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4 md:gap-6">
          <div v-for="(cert, index) in displayedCertificates" :key="'cert-' + index"
            class="group bg-white rounded-xl shadow-md hover:shadow-xl transition-all duration-300 overflow-hidden border border-gray-100 hover:border-gray-200 flex flex-col">
            <div class="relative overflow-hidden">
              <img :src="cert.image" :alt="cert.title"
                class="w-full h-32 md:h-40 object-cover transition-transform duration-300 group-hover:scale-105">
              <div class="absolute top-2 left-2">
                <span
                  :class="`inline-flex items-center px-2 py-1 rounded-full text-xs font-semibold bg-gradient-to-r ${cert.gradient} text-white shadow-md`">
                  {{ cert.issuer }}
                </span>
              </div>
              <div class="absolute top-2 right-2">
                <div class="w-6 h-6 bg-white rounded-full flex items-center justify-center">
                  <svg class="w-4 h-4 text-yellow-500" fill="currentColor" viewBox="0 0 20 20">
                    <path
                      d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
                  </svg>
                </div>
              </div>
            </div>
            <div class="p-3 md:p-4 flex-1 flex flex-col">
              <h4 class="font-semibold text-sm md:text-base text-gray-800 mb-2 line-clamp-2">{{ cert.title }}</h4>
              <p class="text-gray-600 text-xs md:text-sm flex-1 leading-relaxed mb-3 line-clamp-3">{{ cert.description
                }}</p>
              <div class="space-y-2">
                <a :href="cert.url" target="_blank"
                  :class="`w-full  flex h-8 items-center justify-center md:h-10 bg-gradient-to-r ${cert.gradient} text-white rounded-lg text-xs md:text-sm font-medium transition-all duration-300`">
                  View Certificate
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- News About Me Section -->
      <div class="mb-16">
        <div class="flex items-center justify-between mb-8">
          <h3 class="text-2xl md:text-3xl font-bold text-gray-800">News About Me</h3>
          <button v-if="newsData.length > 2" @click="toggleNewsExpanded"
            class="flex items-center gap-2 px-4 py-2 bg-gray-100 hover:bg-gray-200 rounded-lg transition-all duration-300">
            <span class="text-gray-600 font-medium">{{ newsExpanded ? 'Show Less' : 'Show More' }}</span>
            <svg :class="['w-4 h-4 text-gray-600 transition-transform duration-300', newsExpanded ? 'rotate-180' : '']"
              fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7"></path>
            </svg>
          </button>
        </div>

        <!-- News Grid -->
        <div class="grid grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4 md:gap-6">
          <div v-for="(news, index) in displayedNews" :key="'news-' + index"
            class="group bg-white rounded-xl shadow-md hover:shadow-xl transition-all duration-300 overflow-hidden border border-gray-100 hover:border-gray-200 flex flex-col">
            <div class="relative overflow-hidden">
              <img :src="news.image" :alt="news.title"
                class="w-full h-32 md:h-40 object-cover transition-transform duration-300 group-hover:scale-105">
              <div class="absolute top-2 left-2">
                <span
                  :class="`inline-flex items-center px-2 py-1 rounded-full text-xs font-semibold bg-gradient-to-r ${news.gradient} text-white shadow-md`">
                  {{ news.category }}
                </span>
              </div>
            </div>
            <div class="p-3 md:p-4 flex-1 flex flex-col">
              <h4 class="font-semibold text-sm md:text-base text-gray-800 mb-2 line-clamp-2">{{ news.title }}</h4>
              <p class="text-gray-600 text-xs md:text-sm flex-1 leading-relaxed mb-3 line-clamp-3"
                v-html="news.description"></p>
              <button @click="openPopup(news)"
                :class="`w-full h-8 md:h-10 bg-gradient-to-r ${news.gradient} text-white rounded-lg text-xs md:text-sm font-medium transition-all duration-300`">
                Read More
              </button>
            </div>
          </div>
        </div>
      </div>
      <div v-if="showPopup" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50">
        <div class="bg-white rounded-xl shadow-lg max-w-md w-[90%]  p-6 relative">
          <button class="absolute top-2 right-2 text-gray-500 hover:text-gray-700" @click="showPopup = false">
            ✕
          </button>
          <h3 class="text-lg font-semibold mb-4">Lihat berita terkait</h3>
          <div class="space-y-3">
            <a v-for="(link, i) in activeNews.url" :key="'link-' + i" :href="link.url" target="_blank"
              rel="noopener noreferrer"
              class="block w-full px-4 py-2 bg-purple-500 hover:bg-purple-600 text-white rounded-lg text-sm font-medium text-center">
              {{ link.title }}
            </a>
          </div>
        </div>
      </div>


    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      newsExpanded: false,
      certificatesExpanded: false,
      showPopup: false,
      newsData: [
        {
          title: "Pagar sakti - Aplikasi anti bullying",
          description: "<strong>Cabang Dinas Kota Magelang</strong> requested me to create an API for the application in the backend part",
          image: "news/pagarSakti.png",
          url: [
            {
              url: "https://smkn2mgl.sch.id/read/570/aplikasi-anti-bullying-pagar-sakti",
              title: "Kontribusi saya"
            },
            {
              url: "https://pdk.jatengprov.go.id/index.php/2024/08/06/pagar-sakti-solusi-pintar-cegah-kekerasan-di-sekolah/",
              title: "Jateng Prov - Pagar Sakti"
            }
          ],
          category: "School Achievement",
          gradient: "from-purple-500 to-purple-600"
        }
      ],

      certificatesData: [
        {
          title: "Unity Certified Developer",
          description: "Official certification demonstrating proficiency in Unity game engine development and best practices...",
          image: "sertif/thumb/Unity.png",
          issuer: "Unity",
          url: "sertif/Unity.pdf",
          gradient: "from-gray-600 to-gray-700"
        },
        {
          title: "Vue JS Certified",
          description: "Official Vue Js Training Certificate from sanbercode",
          image: "sertif/thumb/Vue.png",
          issuer: "Vue Js",
          url: "https://sanbercode.com/certificate/in/c3ffafc0-97fd-4c6a-a2e9-7390d96bdb87",
          gradient: "from-blue-600 to-blue-700"
        }
      ]
    }
  },

  computed: {
    displayedNews() {
      if (this.newsExpanded) {
        return this.newsData;
      }
      // Show first row only (4 items on desktop, 3 on tablet, 2 on mobile)
      return this.newsData.slice(0, 4);
    },

    displayedCertificates() {
      if (this.certificatesExpanded) {
        return this.certificatesData;
      }
      // Show first row only (4 items on desktop, 3 on tablet, 2 on mobile)
      return this.certificatesData.slice(0, 4);
    }
  },

  methods: {
    toggleNewsExpanded() {
      this.newsExpanded = !this.newsExpanded;
    },

    toggleCertificatesExpanded() {
      this.certificatesExpanded = !this.certificatesExpanded;
    },
    openPopup(news) {
      this.activeNews = news;
      this.showPopup = true;
    },
  }
}
</script>
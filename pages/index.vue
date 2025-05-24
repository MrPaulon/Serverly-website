<template>
  <div class="min-h-screen flex flex-col text-indigo-100 relative">
    <!-- Navbar flottante -->
    <nav
      style="background-color: rgb(30 38 53 / 80%); backdrop-filter: blur(10px);"
      class="fixed top-6 left-1/2 transform -translate-x-1/2 w-11/12 max-w-4xl bg-opacity-80 backdrop-blur-md rounded-2xl px-4 py-3 flex items-center justify-between shadow-lg z-50 md:px-8"
    >
      <!-- Logo + Nom -->
      <div class="flex items-center space-x-3">
        <img src="/logo.png" alt="Logo" class="h-10 w-10 object-contain" />
        <span class="text-indigo-200 font-semibold text-xl select-none">Serverly</span>
      </div>

      <!-- Boutons desktop -->
      <div class="hidden md:flex flex-row items-center space-x-4 text-indigo-300 font-medium">
        <UButton icon="solar:document-bold-duotone" size="lg" color="primary" variant="subtle" to="/" style="color: var(--color-text);">Documentation</UButton>
        <UButton icon="line-md:github-twotone" size="lg" color="primary" variant="subtle" to="https://github.com/mrpaulon/serverly" style="color: var(--color-text);">Github</UButton>
        <UButton icon="ic:sharp-discord" size="lg" color="primary" variant="subtle" to="https://discord.gg/BmvNZKMHV2" style="color: var(--color-text);">Discord</UButton>
      </div>

      <!-- Hamburger menu mobile -->
      <button
        @click="toggleMenu"
        class="block md:hidden text-indigo-300 focus:outline-none"
        aria-label="Toggle menu"
      >
        <svg class="h-8 w-8" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" viewBox="0 0 24 24">
          <path v-if="!isMenuOpen" d="M4 6h16M4 12h16M4 18h16" />
          <path v-else d="M6 18L18 6M6 6l12 12" />
        </svg>
      </button>
    </nav>

    <!-- Menu drawer mobile -->
    <transition name="fade">
      <div
        v-if="isMenuOpen"
        style="background-color: var(--color-background);"
        class="fixed top-0 left-0 w-full h-screen bg-opacity-95 backdrop-blur-md z-40 flex flex-col items-center justify-center space-y-8 text-indigo-100 text-xl font-semibold"
      >
        <UButton icon="solar:document-bold-duotone" size="xl" color="primary" variant="solid" to="/" style="color: var(--color-text);">Documentation</UButton>
        <UButton icon="line-md:github-twotone" size="xl" color="primary" variant="solid" to="https://github.com/mrpaulon/serverly" style="color: var(--color-text);">Github</UButton>
        <UButton icon="ic:sharp-discord" size="xl" color="primary" variant="solid" to="https://discord.gg/BmvNZKMHV2" style="color: var(--color-text);">Discord</UButton>

        <UButton @click="toggleMenu" size="xl" color="primary" variant="subtle" style="color: var(--color-text);">Fermer</UButton>
      </div>
    </transition>

    <!-- Hero -->
    <section style="background-color: var(--color-background);" class="py-30 px-6 text-center hero-texture">
      <div class="blur-bg" ref="blurRef"></div>
      <div class="max-w-3xl mx-auto">
        <h1 class="text-4xl md:text-5xl pt-20 font-bold mb-6 text-indigo-300">
          Gérez vos serveurs simplement.
        </h1>
        <p class="text-lg md:text-xl mb-8 text-indigo-200">
          Une interface moderne pour monitorer, contrôler et automatiser vos serveurs.
        </p>
        <UButton icon="solar:document-bold" size="xl" color="primary" variant="solid" to="/" style="color: var(--color-text);" class="mt-4 text-xl px-5 py-3">Voir la documentation</UButton>
      </div>
    </section>

    <!-- Features -->
    <section style="background-color: var(--color-background);" class="py-16 px-6">
      <div class="max-w-6xl mx-auto grid md:grid-cols-3 gap-10">
        <div style="background-color: var(--color-surface);" class="rounded-xl p-12 shadow-lg text-center feature-texture">
          <div class="mb-4">
            <UIcon style="width: 40px; height: 40px; color: var(--color-primary);" name="solar:eye-bold-duotone" class="size-12" />
          </div>
          <h3 class="text-xl font-semibold mb-2 text-indigo-200">Surveillance en temps réel</h3>
          <p class="text-gray-400">Visualisez l'état de vos serveurs instantanément.</p>
        </div>
        <div style="background-color: var(--color-surface);" class="rounded-xl p-12 shadow-lg text-center feature-texture">
          <div class="mb-4">
            <UIcon style="width: 40px; height: 40px; color: var(--color-primary);" name="solar:code-square-bold-duotone" class="size-12" />
          </div>
          <h3 class="text-xl font-semibold mb-2 text-indigo-200">Automatisations</h3>
          <p class="text-gray-400">Déclenchez des actions automatiquement selon vos règles.</p>
        </div>
        <div style="background-color: var(--color-surface);" class="rounded-xl p-12 shadow-lg text-center feature-texture">
          <div class="mb-4">
            <UIcon style="width: 40px; height: 40px; color: var(--color-primary);" name="solar:monitor-bold-duotone" class="size-12" />
          </div>
          <h3 class="text-xl font-semibold mb-2 text-indigo-200">Tableau de bord intuitif</h3>
          <p class="text-gray-400">Une UI claire, pensée pour les admins.</p>
        </div>
      </div>
    </section>

    <section style="background-color: var(--color-background);" class="py-16 px-6 text-center max-w-4xl mx-auto">
      <h2 class="text-3xl font-bold text-indigo-300 mb-6">Pourquoi choisir Serverly ?</h2>
      <p class="text-indigo-200 text-lg leading-relaxed">
        Serverly vous offre une plateforme intuitive et puissante pour gérer vos serveurs avec facilité. Profitez d’une surveillance en temps réel, d’automatisations avancées, et d’un tableau de bord pensé pour les administrateurs.
      </p>
    </section>

    <!-- Gallery -->
    <section style="background-color: var(--color-background); display: flex; justify-content: center;" class="py-16 px-6 gallery-texture">
      <UCarousel
        class="w-full max-w-5xl mx-auto px-4 sm:px-6"
        arrows
        v-slot="{ item }"
        :items="carouselItems"
        :ui="uiProp"
      >
        <img
          :src="item"
          width="450"
          height="300"
          class="rounded-lg cursor-pointer"
          @click="openImage(item)"
          alt="Aperçu serveur"
        />
      </UCarousel>
    </section>

    <transition name="fade">
      <div
        v-if="selectedImage"
        class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-75 cursor-pointer"
        @click.self="closeImage"
      >
        <img
          :src="selectedImage"
          alt="Image agrandie"
          class="max-w-4xl max-h-[90vh] rounded-lg shadow-lg"
        />
        <button
          @click="closeImage"
          aria-label="Fermer"
          class="absolute top-6 right-6 text-white bg-gray-900 bg-opacity-60 rounded-full p-2 hover:bg-opacity-80"
        >
          ✕
        </button>
      </div>
    </transition>

    <section class="py-20 px-6 text-center gallery-texture text-indigo-100">
      <div class="max-w-3xl mx-auto flex flex-col items-center gap-6">
        <img src="/logo.png" alt="Serverly Logo" class="w-40 h-40 object-contain" />
        <h2 class="text-3xl font-bold">The Future of Easy Hosting</h2>
        <UButton
          to="/"
          size="lg"
          color="primary"
          variant="solid"
          class="mt-4 px-8 py-3 text-lg"
          style="color: var(--color-text);"
          icon="solar:cloud-bold-duotone"
        >
          Démarrer maintenant
        </UButton>
      </div>
    </section>

    <!-- Footer -->
    <footer style="background-color: var(--color-surface); color: var(--color-text); font-weight: bold;" class="py-6 text-center text-sm mt-auto">
      © 2025 - Serverly. Tous droits réservés.
    </footer>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue'

const isMenuOpen = ref(false)

function toggleMenu() {
  isMenuOpen.value = !isMenuOpen.value
}

const windowWidth = ref(0)

function updateWidth() {
  windowWidth.value = window.innerWidth
}

onMounted(() => {
  windowWidth.value = window.innerWidth
  window.addEventListener('resize', updateWidth)
})

onUnmounted(() => {
  window.removeEventListener('resize', updateWidth)
})

const uiProp = computed(() => {
  if (windowWidth.value < 768) {
    return { item: 'basis-1/1' } // mobile
  }
  return { item: 'basis-1/3' } // desktop
})

const carouselItems = [
  'dashboard.png',
  'webconsole.png',
  'auth.png',
  'admin.png',
  'server_creation1.png',
  'server_creation2.png',
]

const selectedImage = ref<string | null>(null)

function openImage(img: string) {
  selectedImage.value = img
}

function closeImage() {
  selectedImage.value = null
}
</script>

<style scoped>
.hero-texture {
  background-image: radial-gradient(rgba(255 255 255 / 0.1) 1px, transparent 1px);
  background-size: 20px 20px;
}

.gallery-texture {
  background-image: radial-gradient(rgba(255 255 255 / 0.1) 1px, transparent 1px);
  background-size: 20px 20px;
}

.blur-bg {
  position: absolute;
  top: 80%;
  left: 50%;
  width: 400px;
  height: 400px;
  background: radial-gradient(circle at 30% 30%, rgba(99, 102, 241, 0.6), transparent 60%);
  filter: blur(80px);
  animation: moveBlur 40s linear infinite;
  z-index: 0;
  pointer-events: none;
  border-radius: 50%;
}

section.hero-texture {
  position: relative;
  overflow: hidden;
  z-index: 1;
}

@keyframes moveBlur {
  0% {
    transform: translate(-20%, -20%);
  }
  25% {
    transform: translate(40%, -40%);
  }
  50% {
    transform: translate(-20%, -20%);
  }
  75% {
    transform: translate(-80%, -40%);
  }
  100% {
    transform: translate(-20%, -20%);
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>
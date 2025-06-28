<template>
  <div class="min-h-screen bg-[#121212] text-white font-sans">
    <!-- Navbar -->
    <nav class="bg-[#1f1f1f] border-b border-[#e10600] shadow-md">
      <div class="max-w-6xl mx-auto px-6 py-4 flex justify-between items-center">
        <div class="text-2xl font-extrabold text-[#f44336] tracking-wide select-none drop-shadow-[0_2px_5px_rgba(244,67,54,0.8)]">
          F1 Fantasy
        </div>
        <div class="space-x-6 flex items-center">
          <button
            v-if="user"
            @click="logout"
            class="px-4 py-2 bg-[#f44336] hover:bg-[#d32f2f] rounded font-semibold transition-colors duration-300"
          >
            Cerrar sesión
          </button>
        </div>
      </div>
    </nav>

    <!-- Contenido principal -->
    <main class="max-w-4xl mx-auto p-10">
      <Login v-if="!user" @login-success="onLoginSuccess" />

      <div v-else>
        <h1 class="text-4xl font-extrabold text-[#f44336] mb-8 tracking-wide drop-shadow-[0_2px_5px_rgba(244,67,54,0.8)]">
          Bienvenido, {{ user }} a la Web de F1 🏎️
        </h1>
        <p class="text-gray-300 leading-relaxed mb-8 text-lg">
          ¡Aquí encontrarás noticias, estadísticas y todo lo que necesitas para tu Fantasy F1!
        </p>

        <button
          @click="mostrarNormas = !mostrarNormas"
          class="px-5 py-3 bg-[#f4511e] hover:bg-[#bf360c] rounded-lg font-semibold transition-colors duration-300"
        >
          {{ mostrarNormas ? 'Ocultar Normas' : 'Ver Normas del Fantasy F1' }}
        </button>

        <transition name="fade">
          <div v-if="mostrarNormas" class="mt-10">
            <NormasF1 />
          </div>
        </transition>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Login from './components/Login.vue'
import NormasF1 from './components/NormasF1.vue' // Aquí pones el componente de las normas que te pasé antes

const user = ref(localStorage.getItem('user'))
const mostrarNormas = ref(false)

function onLoginSuccess(username) {
  user.value = username
  localStorage.setItem('user', username)
  mostrarNormas.value = false
}

function logout() {
  user.value = null
  localStorage.removeItem('user')
  mostrarNormas.value = false
}
</script>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

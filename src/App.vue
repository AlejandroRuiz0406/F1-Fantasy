<template>
  <div>
    <Login v-if="!user" @login-success="handleLogin" />
    <div v-else class="min-h-screen bg-gradient-to-b from-gray-900 via-gray-800 to-black text-white">
      <nav class="flex items-center justify-between bg-gradient-to-r from-red-900 to-black px-6 py-4 shadow-lg">
        <a
          href="#"
          @click.prevent="currentView = 'inicio'"
          class="text-2xl font-extrabold tracking-widest text-red-600 hover:text-red-400 transition"
        >
          Fantasy F1
        </a>
        <div class="space-x-4">
          <button
            @click="currentView = 'inicio'"
            :class="buttonClass(currentView === 'inicio')"
          >
            Inicio
          </button>
          <button
            @click="currentView = 'normas'"
            :class="buttonClass(currentView === 'normas')"
          >
            Normas
          </button>
          <button
            @click="logout"
            class="px-4 py-2 rounded bg-red-700 hover:bg-red-600 transition"
          >
            Cerrar sesión
          </button>
        </div>
      </nav>

      <main class="p-8 max-w-5xl mx-auto">
        <h1 class="text-4xl font-bold mb-8 text-red-500 drop-shadow-lg">
          Bienvenido, {{ user }} a la Web de F1 🏎️
        </h1>
        <Inicio v-if="currentView === 'inicio'" />
        <NormasFantasyF1 v-else-if="currentView === 'normas'" />
      </main>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Login from './components/Login.vue'
import Inicio from './components/Inicio.vue'
import NormasFantasyF1 from './components/NormasFantasyF1.vue'

const user = ref(null)
const currentView = ref('inicio')

onMounted(() => {
  user.value = localStorage.getItem('user')
})

const handleLogin = (username) => {
  user.value = username
  localStorage.setItem('user', username)
  currentView.value = 'inicio'
}

const logout = () => {
  localStorage.removeItem('user')
  user.value = null
}

const buttonClass = (active) =>
  active
    ? 'px-4 py-2 rounded bg-red-600 text-white font-semibold shadow-md hover:bg-red-500 transition'
    : 'px-4 py-2 rounded bg-transparent border border-red-600 text-red-400 hover:bg-red-700 hover:text-white transition'
</script>

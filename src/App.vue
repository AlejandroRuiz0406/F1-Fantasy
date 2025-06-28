<template>
  <div>
    <Login v-if="!user" @login-success="handleLogin" />
    <div v-else>
      <nav
        class="navbar navbar-expand-lg"
        :class="['px-4', 'bg-gradient-to-r', 'from-gray-900', 'via-gray-800', 'to-black', 'border-b-2', 'border-red-700']"
      >
        <a
          class="navbar-brand text-red-600 font-extrabold cursor-pointer hover:text-red-400"
          href="#"
          @click.prevent="currentView = 'inicio'"
        >
          Fantasy F1
        </a>
        <div class="ml-auto">
          <button
            class="btn btn-outline-light mx-2 text-red-400 hover:text-red-600 border-red-600 hover:border-red-700"
            :class="{ 'btn-active': currentView === 'inicio' }"
            @click="currentView = 'inicio'"
          >
            Inicio
          </button>
          <button
            class="btn btn-outline-light mx-2 text-red-400 hover:text-red-600 border-red-600 hover:border-red-700"
            :class="{ 'btn-active': currentView === 'normas' }"
            @click="currentView = 'normas'"
          >
            Normas
          </button>
          <button
            class="btn btn-outline-light mx-2 text-red-400 hover:text-red-600 border-red-600 hover:border-red-700"
            @click="logout"
          >
            Cerrar sesión
          </button>
        </div>
      </nav>

      <div class="p-6 bg-gradient-to-b from-gray-900 via-gray-800 to-black min-h-screen text-gray-100">
        <h1 class="text-4xl font-bold mb-6 text-red-600 drop-shadow-lg">
          Bienvenido, {{ user }} a la Web de F1 🏎️
        </h1>
        <Inicio v-if="currentView === 'inicio'" />
        <NormasFantasyF1 v-else-if="currentView === 'normas'" />
      </div>
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
</script>

<style>
.btn-active {
  background-color: #b91c1c; /* rojo intenso */
  color: white !important;
  border-color: #991b1b !important;
}
</style>

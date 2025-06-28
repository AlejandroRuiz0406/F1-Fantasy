<template>
  <div>
    <Login v-if="!user" @login-success="handleLogin" />

    <div v-else class="min-vh-100 bg-dark text-light">
      <!-- Navbar -->
      <nav class="navbar navbar-expand-lg navbar-dark bg-danger bg-gradient shadow-sm px-4">
        <div class="container-fluid">
          <a class="navbar-brand fw-bold" href="#" @click.prevent="currentView = 'inicio'">
            🏁 Fantasy F1
          </a>
          <div class="d-flex">
            <button
              @click="currentView = 'inicio'"
              :class="buttonClass(currentView === 'inicio')"
            >
              Inicio
            </button>
            <button
              @click="currentView = 'normas'"
              :class="buttonClass(currentView === 'normas')"
              class="ms-2"
            >
              Normas
            </button>
            <button
              @click="logout"
              class="btn btn-outline-light ms-3"
            >
              Cerrar sesión
            </button>
          </div>
        </div>
      </nav>

      <!-- Main -->
      <main class="container py-5">
        <h1 class="display-5 fw-bold text-center text-warning mb-5">
          Bienvenido, {{ user }} 🚥 A la Web de F1
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
    ? 'btn btn-light fw-semibold'
    : 'btn btn-outline-light'

</script>

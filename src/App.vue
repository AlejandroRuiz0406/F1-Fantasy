<template>
  <div>
    <Login v-if="!user" @login-success="handleLogin" />
    <div v-else>
      <nav class="navbar navbar-expand-lg navbar-dark bg-dark px-4">
        <a class="navbar-brand" href="#" @click="currentView = 'inicio'">Fantasy F1</a>
        <div class="ml-auto">
          <button class="btn btn-outline-light mx-2" @click="currentView = 'inicio'">Inicio</button>
          <button class="btn btn-outline-light mx-2" @click="currentView = 'normas'">Normas</button>
          <button class="btn btn-outline-light mx-2" @click="logout">Cerrar sesión</button>
        </div>
      </nav>

      <div class="p-6">
        <h1 class="text-4xl font-bold mb-6">Bienvenido, {{ user }} a la Web de F1 🏎️</h1>
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

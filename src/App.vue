<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark px-4">
      <a class="navbar-brand" href="#" @click="currentView = 'inicio'">Fantasy F1</a>
      <div class="ml-auto">
        <button class="btn btn-outline-light mx-2" @click="currentView = 'inicio'">Inicio</button>
        <button class="btn btn-outline-light mx-2" @click="currentView = 'normas'">Normas</button>
        <button class="btn btn-outline-light mx-2" @click="currentView = 'login'">Login</button>
      </div>
    </nav>

    <Login v-if="currentView === 'login'" @login-success="currentView = 'inicio'" />
    <Inicio v-else-if="currentView === 'inicio'" />
    <NormasFantasyF1 v-else-if="currentView === 'normas'" />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Login from './components/Login.vue'
import NormasFantasyF1 from './components/NormasFantasyF1.vue'
import Inicio from './components/Inicio.vue'

const currentView = ref('login')
</script>

<template>
  <div>
    <Login v-if="!user" />
    <div v-else class="p-6">
      <h1 class="text-4xl font-bold mb-6">Bienvenido, {{ user }} a la Web de F1 🏎️</h1>
      <button
        @click="logout"
        class="mb-4 px-4 py-2 bg-gray-700 text-white rounded hover:bg-gray-800"
      >
        Cerrar sesión
      </button>
      <!-- Aquí va el contenido principal de la web -->
      <p>¡Aquí irán las noticias, estadísticas y más!</p>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import Login from './components/Login.vue'

const user = ref(null)

onMounted(() => {
  user.value = localStorage.getItem('user')
})

const logout = () => {
  localStorage.removeItem('user')
  user.value = null
}
</script>

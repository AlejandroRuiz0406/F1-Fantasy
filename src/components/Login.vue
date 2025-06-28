<template>
  <div class="min-h-screen flex items-center justify-center bg-gradient-to-r from-red-600 to-yellow-400">
    <div class="bg-white rounded-lg shadow-lg p-8 max-w-md w-full">
      <h2 class="text-3xl font-bold mb-6 text-center text-gray-800">Iniciar Sesión - F1 Web</h2>
      <form @submit.prevent="login">
        <div class="mb-4">
          <label class="block text-gray-700 mb-2" for="username">Usuario</label>
          <input
            v-model="username"
            id="username"
            type="text"
            placeholder="Usuario"
            class="w-full border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring-2 focus:ring-red-500"
            required
          />
        </div>
        <div class="mb-6">
          <label class="block text-gray-700 mb-2" for="password">Contraseña</label>
          <input
            v-model="password"
            id="password"
            type="password"
            placeholder="Contraseña"
            class="w-full border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring-2 focus:ring-red-500"
            required
          />
        </div>
        <p v-if="error" class="text-red-600 mb-4 text-center">{{ error }}</p>
        <button
          type="submit"
          class="w-full bg-red-600 text-white font-semibold py-2 rounded hover:bg-red-700 transition"
        >
          Entrar
        </button>
      </form>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const username = ref('')
const password = ref('')
const error = ref(null)

const users = {
  Jorge: 'password123',
  López: 'secret456',
  Dani: 'f1rocks',
  Ruiz: 'fastlane',
}

const login = () => {
  error.value = null
  if (users[username.value] && users[username.value] === password.value) {
    localStorage.setItem('user', username.value)
    window.location.reload() // recarga para mostrar contenido autenticado
  } else {
    error.value = 'Usuario o contraseña incorrectos'
  }
}
</script>

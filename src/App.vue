<template>
  <div>
    <h1>¡Hola! Esta es la página principal</h1>
    <button @click="fetchMessage">Obtener mensaje del backend</button>
    <p>{{ message }}</p>
  </div>
</template>

<script setup>
import { ref } from 'vue'
const message = ref('')

const fetchMessage = async () => {
  const res = await fetch('/api/hello')
  const data = await res.json()
  message.value = data.message
}
</script>

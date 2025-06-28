<template>
  <div class="bg-black text-white min-h-screen py-12 px-6 flex justify-center">
    <div class="max-w-3xl w-full">
      <h1 class="text-4xl font-bold text-red-600 mb-8 text-center">
        🏎️ Normas Fantasy F1
      </h1>

      <div class="space-y-8">
        <div
          v-for="(norma, index) in normas"
          :key="index"
          class="bg-gray-900 p-5 rounded-lg shadow-lg border border-red-600 hover:border-red-500 transition"
        >
          <h2 class="text-2xl font-semibold text-red-400 mb-3">Norma {{ index + 1 }}</h2>
          <p class="text-gray-300 whitespace-pre-line leading-relaxed">{{ norma }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
const normas = [
  `El "nano sobre": cada semana de carrera lo abre un participante aleatorio (por sorteo). El sobre puede contener:

- Aplicar un chip.
- Quitarle a alguien un piloto (que no sea del top 5 de escuderías).
- Prohibir a otro usar pilotos del top 5 (los 2 mejores) en su alineación esa carrera.
- Veto a un piloto de otro durante 2 carreras.
- Veto al piloto con DRS del que abrió el sobre.
- Opción vacía (no se aplica nada).`,

  `Si un participante tiene un piloto que no es del top 4 de escuderías y queda en el top 4 del GP, puede elegir a qué rival quitarle una escudería por una carrera (la escudería sustituta se elige por sorteo).`,

  `Si un participante tiene un piloto que no es del top 4 de escuderías y queda en el top 8 del GP, puede elegir quitarle el x2 de un piloto a otro rival para la siguiente carrera.`,

  `Si un participante tiene un piloto (que no sea de Red Bull, Ferrari, Mercedes o McLaren) que queda primero en la qualy, podrá quitarle 2 pilotos a otro en la siguiente carrera. Uno será elegido por él y el otro por sorteo.`
]
</script>

<style scoped>
/* Evita scroll horizontal */
html, body {
  overflow-x: hidden;
}
</style>

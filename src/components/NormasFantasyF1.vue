<template>
  <div class="bg-black text-white min-h-screen py-12 px-6">
    <div class="max-w-4xl mx-auto">
      <h1 class="text-4xl font-bold text-red-600 mb-8 text-center">
        🏎️ Normas Fantasy F1
      </h1>

      <div class="space-y-8">
        <div v-for="(norma, index) in normas" :key="index" class="bg-gray-900 p-6 rounded-lg shadow-md border border-red-600">
          <h2 class="text-2xl font-semibold text-red-400 mb-2">Norma {{ index + 1 }}</h2>
          <p class="text-gray-200 whitespace-pre-line">{{ norma }}</p>
        </div>
      </div>

      <div class="text-center mt-12">
        <img
          src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/33/F1.svg/2560px-F1.svg.png"
          alt="F1 logo"
          class="w-40 mx-auto opacity-70"
        />
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

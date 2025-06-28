<template>
  <div class="min-h-screen bg-[#121212] text-white py-16 px-6 flex justify-center">
    <div class="max-w-3xl w-full bg-[#1f1f1f] rounded-lg shadow-lg border border-[#e10600] p-10">
      <h1 class="text-4xl font-extrabold text-[#f44336] mb-12 text-center tracking-wide drop-shadow-[0_2px_5px_rgba(244,67,54,0.8)] font-sans">
        🏎️ Normas Fantasy F1
      </h1>

      <div class="space-y-10">
        <section
          v-for="(norma, index) in normas"
          :key="index"
          class="bg-[#292929] border border-[#d84315] rounded-lg p-6 shadow-md hover:shadow-[#f4511e] transition-shadow duration-300"
        >
          <h2 class="text-2xl font-semibold text-[#ff7043] mb-4 tracking-wide drop-shadow-[0_1px_3px_rgba(255,112,67,0.7)] font-sans">
            Norma {{ index + 1 }}
          </h2>
          <p class="text-gray-300 whitespace-pre-line leading-relaxed font-medium tracking-wide font-sans">
            {{ norma }}
          </p>
        </section>
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

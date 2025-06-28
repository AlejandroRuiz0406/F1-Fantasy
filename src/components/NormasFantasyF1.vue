<template>
  <div class="bg-dark text-light py-5 min-vh-100">
    <div class="container" style="max-width: 850px;">
      <div class="bg-black bg-gradient border border-danger rounded-4 shadow-lg p-5">
        <h1 class="display-4 fw-bold text-center text-danger mb-5">
          🏎️ Normas Fantasy F1
        </h1>

        <div class="accordion" id="accordionNormas">
          <div
            class="accordion-item bg-dark border border-secondary text-light mb-3"
            v-for="(norma, index) in normas"
            :key="index"
          >
            <h2 class="accordion-header">
              <button
                class="accordion-button collapsed bg-danger bg-gradient text-light fw-semibold"
                type="button"
                data-bs-toggle="collapse"
                :data-bs-target="'#norma' + index"
              >
                Norma {{ index + 1 }}
              </button>
            </h2>
            <div
              :id="'norma' + index"
              class="accordion-collapse collapse"
              data-bs-parent="#accordionNormas"
            >
              <div class="accordion-body text-break">
                <div style="white-space: pre-line;">{{ norma }}</div>
              </div>
            </div>
          </div>
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

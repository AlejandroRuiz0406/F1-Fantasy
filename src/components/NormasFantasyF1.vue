<template>
  <div class="container py-5 text-white" style="background-color: #0c0c0c; min-height: 100vh;">
    <h1 class="text-center mb-5 display-4 text-danger">🏁 Normas Oficiales del Fantasy F1</h1>

    <div class="card bg-dark mb-4 shadow-lg border border-danger">
      <div class="card-body">
        <h3 class="card-title text-danger">1. 🧨 El Sobre del Nano</h3>
        <p class="card-text">
          Cada semana de carrera, uno de los participantes será elegido al azar para <strong>abrir el sobre del Nano</strong>, que puede contener:
        </p>
        <ul>
          <li>💡 Aplicar un chip especial.</li>
          <li>🔁 Robar un piloto a otro jugador (no del Top 5 de escuderías).</li>
          <li>🚫 Prohibir a otro usar pilotos del Top 5 para esa carrera.</li>
          <li>❌ Vetar un piloto rival durante 2 Grandes Premios.</li>
          <li>🛑 Anular el piloto con impulso DRS del jugador que abre el sobre.</li>
          <li>📭 Sobre vacío: no se activa ninguna acción.</li>
        </ul>
      </div>
    </div>

    <div class="card bg-dark mb-4 shadow-lg border border-danger">
      <div class="card-body">
        <h3 class="card-title text-danger">2. 🏎️ Piloto Revelación en el Top 4</h3>
        <p class="card-text">
          Si un jugador tiene un piloto <strong>fuera del Top 4 de escuderías</strong> y este queda <strong>en el Top 4 del GP</strong>, podrá quitarle una escudería a un rival por una carrera. La escudería sustituta se elegirá por sorteo.
        </p>
      </div>
    </div>

    <div class="card bg-dark mb-4 shadow-lg border border-danger">
      <div class="card-body">
        <h3 class="card-title text-danger">3. ✖️ Bloqueo del Doble Puntuación</h3>
        <p class="card-text">
          Si un piloto <strong>fuera del Top 4</strong> queda entre los <strong>8 primeros</strong> del GP:
          su mánager podrá <strong>anular el x2</strong> de un piloto rival en la siguiente carrera.
        </p>
      </div>
    </div>

    <div class="card bg-dark mb-4 shadow-lg border border-danger">
      <div class="card-body">
        <h3 class="card-title text-danger">4. 🎯 Pole Sorpresa</h3>
        <p class="card-text">
          Si un piloto (fuera del Top 4 de escuderías) consigue la <strong>Pole Position</strong>, el mánager podrá quitarle dos pilotos a un rival:
        </p>
        <ul>
          <li>Uno será elegido por el beneficiado.</li>
          <li>El otro será seleccionado por sorteo.</li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script setup>
// No se necesita lógica adicional por ahora
</script>

<style scoped>
ul {
  list-style-type: none;
  padding-left: 0;
}
li::before {
  content: "\2022";
  color: #e10600;
  display: inline-block;
  width: 1em;
  margin-left: -1em;
}
</style>

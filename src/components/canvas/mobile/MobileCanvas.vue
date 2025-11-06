<template>
  <div class="canvas-container">
    <canvas id="mobileCanvas"></canvas>
  </div>
</template>

<script setup>
// placeholder: canvas drawing logic can be added or shared with the desktop canvas
</script>

<style scoped>
.canvas-container {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed; /* fill the viewport */
  top: 0;
  left: 0;
  right: 0;
  bottom: 72px; /* leave space at bottom for the mobile toolbar */
  z-index: 0; /* place canvas beneath toolbar */
}

canvas {
  background: #fff;
  width: 92vw; /* use most of the width on mobile */
  max-width: 720px;
  aspect-ratio: 1/1; /* keeps it square */
  border-radius: 8px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.18);
  z-index: 1; /* sits above container but below toolbar */
}

@media (min-width: 751px) {
  .canvas-container {
    bottom: 0; /* desktop handles toolbar differently */
  }

  canvas {
    width: 40%;
  }
}
</style>

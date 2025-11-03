<template>
    <div class="canvas-container">
        <canvas id="mainCanvas"></canvas>
    </div>
</template>

<style scoped>
    .canvas-container {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;   /* fill the viewport */
    top: 0;
    left: 0;
    width: 100vw;
    height: 110vh;
    z-index: 0; /* place canvas beneath toolbar/sidebar */
    }

    canvas {
    background: #fff;
    width: 40%;          /* adjust size */
    aspect-ratio: 1/1;   /* keeps it square */
    border-radius: 5px;
    box-shadow: 0 0 20px rgba(0,0,0,0.3);
    z-index: 1; /* sits above container but below toolbar/sidebar */
    }
</style>
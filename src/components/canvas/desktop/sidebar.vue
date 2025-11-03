<template>
    <div class="sidebar">
        <div class="color-section">
          <div class="color-wheel"></div>

          <div class="preset-colors">
              <button class="color-swatch" style="background: #ff4d4d;"></button>
              <button class="color-swatch" style="background: #4dff4d;"></button>
              <button class="color-swatch" style="background: #4d4dff;"></button>
              <button class="color-swatch" style="background: #ffff4d;"></button>
              <button class="color-swatch" style="background: #ff4dff;"></button>
              <button class="color-swatch" style="background:#ffffff"></button>
              <button class="color-swatch" style="background:#ffffff"></button>
              <button class="color-swatch" style="background:#ffffff"></button>
              <button class="color-swatch" style="background:#ffffff"></button>
              <button class="color-swatch" style="background:#ffffff"></button>
              <button class="color-swatch" style="background:#ffffff"></button>
              <button class="color-swatch" style="background:#ffffff"></button>
          </div>
        </div>
        <router-link to="/" class="home-btn">Home</router-link>
    </div>
</template>

<style scoped>
  .sidebar {
    position: fixed;
    right: 0;
    top: 100px; /* below top nav */
    width: 220px;
    height: calc(100vh - 100px);
    background: #1e1e1e;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 20px;
    box-shadow: -2px 0 10px rgba(0, 0, 0, 0.3);
    z-index: 30; /* sit above the fixed canvas */
  }

  .color-section {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 20px;
  }

  .color-wheel {
    width: 150px;
    height: 150px;
    border-radius: 50%;
    background: conic-gradient(red, yellow, lime, cyan, blue, magenta, red);
    box-shadow: 0 0 10px rgba(0, 0, 0, 0.4);
    position: relative;
  }

  .color-wheel::after {
    content: "";
    position: absolute;
    inset: 20px;
    background: #1e1e1e;
    border-radius: 50%;
  }

  .preset-colors {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 10px;
  }

  .color-swatch {
    width: 40px;
    height: 40px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: transform 0.2s;
  }

  .color-swatch:hover {
    transform: scale(1.1);
  }

  .color-history {
    width: 100%;
    height: 140px;
    background: #2b2b2b;
    border-radius: 10px;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    color: #aaa;
    font-size: 14px;
    padding: 10px;
  }

  .history-grid {
    margin-top: 6px;
    width: 100%;
    display: grid;
    grid-template-columns: repeat(6, 1fr);
    gap: 6px;
    align-items: center;
    justify-items: center;
  }

  .history-swatch {
    width: 20px;
    height: 20px;
    border: 1px solid rgba(0,0,0,0.12);
    border-radius: 4px;
    padding: 0;
    margin: 0;
  }

  .home-btn {
    display: inline-flex; /* allow anchor to take width/height */
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 60px;
    margin-bottom: 20%;
    background: #2b2b2b;
    border: none;
    border-radius: 10px;
    color: #fff;
    font-size: 16px;
    cursor: pointer;
    transition: background 0.2s, transform 0.2s;
    text-decoration: none;
  }

  .home-btn:hover {
    background: #3a3a3a;
    transform: translateY(-3px);
  }
</style>
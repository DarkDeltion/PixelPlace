<template>
  <div class="mobile-lobby-list-bg">
    <div class="mobile-lobby-list">
      <div class="mobile-lobby-item">
        <div class="mobile-lobby-info">
          <span>Lobby #1</span>
        </div>
        <button class="mobile-lobby-join-btn">Join</button>
      </div>
      <div class="mobile-lobby-item">
        <div class="mobile-lobby-info">
          <span>Lobby #2</span>
        </div>
        <button class="mobile-lobby-join-btn">Join</button>
      </div>
      <div class="mobile-lobby-item">
        <div class="mobile-lobby-info">
          <span>Lobby #3 <span class="mobile-lobby-lock">🔒</span></span>
        </div>
        <button class="mobile-lobby-join-btn">Join</button>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* background container for lobby list */
.mobile-lobby-list-bg {
  width: 100%;
  max-width: 500px;
  margin: 0 auto 1.5rem auto;
  background: #b3b3b3;
  border: 3px solid #222;
  border-radius: 16px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
  padding: 1.2rem 1rem 1.5rem 1rem;
  box-sizing: border-box;
}
/* mobile lobby list */

.mobile-lobby-list {
  display: flex;
  flex-direction: column;
  gap: 0.75rem;
  width: 100%;
  max-width: 500px;
  margin: 0 auto;
}

.mobile-lobby-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: #cfcfcf;
  border: 2px solid #222;
  border-radius: 10px;
  padding: 1rem 1rem;
  font-size: 1.5rem;
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.04);
}

.mobile-lobby-info {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.mobile-lobby-join-btn {
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 1.2rem;
  padding: 0.3rem 1rem;
  border-radius: 8px;
  border: 2px solid #222;
  background: #b3b3b3;
  color: #222;
  cursor: pointer;
  transition: background 0.2s;
}
.mobile-lobby-join-btn:hover {
  background: #d3d3d3;
}

.mobile-lobby-lock {
  font-size: 1.2rem;
  margin-left: 0.5rem;
  margin-right: auto;
}
</style>

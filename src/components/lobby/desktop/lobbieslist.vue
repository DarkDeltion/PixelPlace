<template>
  <div class="lobby-list">
    <div class="lobby-item">
      <span>Lobby #1</span>
      <router-link :to="`/canvas`" class="lobby-join-btn">Join</router-link>
    </div>
    <div class="lobby-item">
      <span>Lobby #2</span>
      <router-link :to="`/canvas`" class="lobby-join-btn">Join</router-link>
    </div>
    <div class="lobby-item">
      <span>Lobby #3 <span class="lobby-lock">🔒</span></span>
      <button class="lobby-join-btn">Join</button>
    </div>
  </div>
</template>

<style scoped>
/* lobby list */
.lobby-list {
  background: #b3b3b3;
  border: 3px solid #222;
  border-radius: 18px;
  padding: 1.5rem;
  margin: 0 2.5rem;
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
}

.lobby-item {
  background: #cfcfcf;
  border: 2px solid #222;
  border-radius: 12px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 1.2rem 1.5rem;
  font-size: 1.7rem;
}

.lobby-join-btn {
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 1.3rem;
  padding: 0.4rem 1.3rem;
  border-radius: 9px;
  border: 2px solid #222;
  background: #b3b3b3;
  color: #222;
  cursor: pointer;
  transition: background 0.2s;
  text-decoration: none;
}

.lobby-join-btn:hover {
  background: #d3d3d3;
}

.lobby-lock {
  font-size: 1.3rem;
  margin-left: 0.5rem;
  margin-right: auto;
}
</style>

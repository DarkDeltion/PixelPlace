<template>
  <div class="mobile-lobby-inputs">
    <input class="mobile-search-bar" type="search" placeholder="Search..." />
    <a class="mobile-create-btn" href="#">Create Canvas</a>
  </div>
</template>

<style scoped>
/* mobile lobby inputs (vertical, desktop colors) */

.mobile-lobby-inputs {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  width: 100%;
  max-width: 500px;
  margin: 0 auto 1.5rem auto;
  box-sizing: border-box;
}

.mobile-search-bar {
  width: 100%;
  min-width: 0;
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 1.5rem;
  padding: 0.5rem 1rem;
  border-radius: 10px;
  border: 2px solid #222;
  background: #888;
  color: #fff;
  outline: none;
  box-sizing: border-box;
  display: block;
}

.mobile-create-btn {
  width: 100%;
  min-width: 0;
  display: block;
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 1.5rem;
  padding: 0.5rem 1rem;
  border-radius: 10px;
  border: 2px solid #222;
  background: #888;
  color: #fff;
  text-decoration: none;
  text-align: center;
  transition: background 0.2s;
  box-sizing: border-box;
}
.mobile-create-btn:hover {
  background: #aaa;
}
</style>

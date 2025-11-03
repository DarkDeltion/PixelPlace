<template>
  <div class="search-bar">
    <input type="search" placeholder="Search..." />
    <a href="#">Create Canvas</a>
  </div>
</template>

<style scoped>
/* search bar */
.search-bar {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin: 2rem 2rem 1rem 2rem;
  gap: 1.5rem;
  flex-wrap: wrap;
}

.search-bar input[type='search'] {
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 1.2em;
  padding: 0.4em 1em;
  border-radius: 0.7em;
  border: 0.13em solid #222;
  background: #888;
  color: #fff;
  outline: none;
  width: 100%;
  max-width: 18em;
  min-width: 8em;
  height: 2.5em;
  box-sizing: border-box;
  flex: 1 1 12em;
}

.search-bar a {
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 1.2em;
  padding: 0.4em 1em;
  border-radius: 0.7em;
  border: 0.13em solid #222;
  background: #888;
  color: #fff;
  text-decoration: none;
  text-align: center;
  transition: background 0.2s;
  height: 2.5em;
  display: flex;
  align-items: center;
  box-sizing: border-box;
  flex: 0 0 auto;
}

.search-bar a:hover {
  background: #aaa;
}
</style>

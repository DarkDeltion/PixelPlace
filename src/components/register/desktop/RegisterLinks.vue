<template>
  <div class="login-links">
    <a href="/forgotpassword">Forgot password?</a>
    <span class="separator">|</span>
    <a href="/login">Account login</a>
  </div>
</template>

<style scoped>
.login-links {
  margin-top: 0.7rem;
  text-align: center;
  width: 100%;
  font-family: 'Pixelify Sans', sans-serif;
  color: #fff;
  font-size: 0.95rem;
}
.login-links a {
  font-family: 'Pixelify Sans', sans-serif;
  color: #fff;
  font-size: 0.95rem;
  text-decoration: none;
  margin: 0 0.2rem;
}
.login-links a:hover {
  text-decoration: underline;
}
.separator {
  color: #fff;
  margin: 0 0.3rem;
  font-size: 0.95rem;
  vertical-align: middle;
  user-select: none;
}
</style>

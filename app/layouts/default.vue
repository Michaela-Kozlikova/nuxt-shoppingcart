<template>
  
  <slot />

  <div class="footer">
    <p>&copy; MADE BY MISHA // ENCRYPTED_DATA_02_2026</p>
  </div>
</template>

<style>
* {
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
  height: 100%;
}

body {
  padding: 10px;
  background:
    radial-gradient(
      circle at 0% 0%,
      rgba(255, 0, 255, 0.2) 0%,
      transparent 40%
    ),
    radial-gradient(
      circle at 100% 100%,
      rgba(255, 0, 255, 0.164) 0%,
      transparent 40%
    ),
    radial-gradient(circle at center, #1e281c 0%, #000000 100%);
  background-size: cover;
  background-attachment: fixed;
  color: white;
  margin: 0;
  font-family: "Share Tech Mono", monospace;
  letter-spacing: 0.02rem;
  cursor: crosshair;
}

.footer {
  display: flex;
  justify-content: center;
  align-items: center;
  color: rgba(155, 254, 7, 0.4);
  border-top: 1px solid rgba(155, 254, 7, 0.1);
  margin: 100px auto 0 auto;
}

.footer p {
  font-size: 0.75rem;
  letter-spacing: 5px;
  padding-left: 5px;
  text-shadow: 0px 0px 2px rgba(155, 254, 7, 0.2);
}
</style>

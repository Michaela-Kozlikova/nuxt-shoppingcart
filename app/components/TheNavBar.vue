<script setup>
import { ref } from "vue";
const navBarItems = [
  { label: "CORE", decode: "[home]" },
  { label: "PINK MARKET", decode: "[e-shop]" },
  { label: "DATABASE", decode: "[about us]" },
  { label: "UPLINK", decode: "[contact]" },
  { label: "BIOMETRICS", decode: "[login]" },
];

const isOpen = ref(false);

const toggleMenu = () => {
  isOpen.value = !isOpen.value;
};
</script>

<template>
  <nav>
    <div
      class="menu-scanner"
      :class="{ active: isOpen }"
      @click="isOpen = !isOpen"
    >
      <div class="scanner-line"></div>
      <span class="scanner-text">[ ACCESS_PORT ]</span>
      <div class="mobile-dots">
        <span></span>
        <span></span>
        <span></span>
      </div>

      <div class="left-nav" :class="{ open: isOpen }">
        <p v-for="(item, index) in navBarItems" :key="index">
          {{ item.label }} <span class="decode">{{ item.decode }}</span>
        </p>
      </div>
    </div>
  </nav>
</template>

<style scoped>
@keyframes scan {
  0% {
    top: 0%;
  }
  100% {
    top: 100%;
  }
}

@keyframes framePulse {
  0%,
  100% {
    border-color: rgba(155, 254, 7, 0.2);
  }
  50% {
    border-color: rgba(155, 254, 7, 0.8);
    box-shadow: 0 0 10px rgba(155, 254, 7, 0.2);
  }
}

.menu-scanner:hover {
  background: rgba(155, 254, 7, 0.1);
  border-color: rgb(155, 254, 7);
}

.left-nav {
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  background: rgba(0, 0, 0, 0.95);
  border-right: 2px solid rgb(155, 254, 7);
  padding: 100px 40px;
  transition: transform 0.4s cubic-bezier(0.165, 0.84, 0.44, 1);
  transform: translateX(-100%);
}

.left-nav p:hover {
  border-radius: 5px;
  transition: all 0.3 ease;
  color: rgb(155, 254, 7);
  padding-left: 20px;
  text-shadow:
    2px 0 rgba(255, 0, 255, 0.7),
    -2px 0 rgba(0, 255, 255, 0.7);
  letter-spacing: 2px;
}

.left-nav p .decode {
  opacity: 0;
  visibility: hidden;
  margin-left: -10px;
  transition: all 0.6s ease;
}

.left-nav p:hover .decode {
  visibility: visible;
  opacity: 1;
  margin-left: 10px;
}

.left-nav.open {
  transform: translateX(0);
}

.menu-scanner {
  top: 20px;
  left: 40px;
  margin-top: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  position: fixed;
  width: 170px;
  height: 40px;
  overflow: hidden;
  transition: all 0.3s ease;
  z-index: 2000;
  animation: framePulse 3s infinite;
  font-size: 0.9rem;
}

.scanner-line {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 2px;
  background: rgb(155, 254, 7);
  box-shadow: 0 0 15px rgb(155, 254, 7);
  animation: scan 3s linear infinite;
  opacity: 0.7;
}

.scanner-text {
  color: rgb(155, 254, 7);
  letter-spacing: 2px;
  z-index: 2;
  text-shadow: 0 0 5px rgb(155, 254, 7);
}
</style>

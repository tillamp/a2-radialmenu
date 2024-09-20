<script setup>
import { ref } from 'vue';

// Reactive variables to store the menu's state and position
const menuVisible = ref(false);
const cursorPositionX = ref(0);
const cursorPositionY = ref(0);

// Function to display or hide the menu at the click position
function displayMenu(event) {
  if (!event.target.closest('.radial-menu')) {
    // Show menu at click position
    cursorPositionX.value = event.clientX; // Get X position
    cursorPositionY.value = event.clientY; // Get Y position
    menuVisible.value = true; // Show radial menu
  } else {
    // Click inside the menu will close it
    menuVisible.value = false;
  }
}
</script>

<template>
  <!-- Full screen area to handle the click -->
  <div class="click-area" @click="displayMenu">
    <!-- Radial Menu -->
    <div
      v-if="menuVisible"
      class="radial-menu"
      :style="{ top: cursorPositionY + 'px', left: cursorPositionX + 'px' }"
      @click.stop
    >
      <div class="menu-item" style="--angle: 0deg">1</div>
      <div class="menu-item" style="--angle: 60deg">2</div>
      <div class="menu-item" style="--angle: 120deg">3</div>
      <div class="menu-item" style="--angle: 180deg">4</div>
      <div class="menu-item" style="--angle: 240deg">5</div>
      <div class="menu-item" style="--angle: 300deg">6</div>
    </div>
  </div>
</template>

<style scoped>
/* Full-screen clickable area */
.click-area {
  width: 100vw;
  height: 100vh;
  position: relative;
}

/* Radial menu styles */
.radial-menu {
  position: absolute;
  width: 150px;
  height: 150px;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
}

/* Menu item styles */
.menu-item {
  width: 40px;
  height: 40px;
  background-color: #3498db;
  color: white;
  text-align: center;
  line-height: 40px;
  border-radius: 50%;
  position: absolute;
  transform: rotate(var(--angle)) translate(75px)
    rotate(calc(-1 * var(--angle)));
}
</style>

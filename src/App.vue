<template>
  <div id="app" @click="handleDocumentClick">
    <!-- Radial Menu -->
    <div
      v-if="showMenu"
      class="radial-menu"
      :style="{ top: `${menuPosition.y}px`, left: `${menuPosition.x}px` }"
    >
      <div
        v-for="(item, index) in menuItems"
        :key="index"
        class="menu-item"
        :style="getItemPosition(index)"
        @click.stop="selectItem(item)"
      >
        {{ item }}
      </div>
    </div>
  </div>
</template>
  
<script>
export default {
  data() {
    return {
      showMenu: false, 
      menuPosition: { x: 0, y: 0 }, // Stores the position of the menu
      menuItems: ["🔊", "🔇", "🗑️", "💾", "📝", "🖨️"], 
    };
  },
  methods: {
    handleDocumentClick(e) {
      // Control the radial menu: open at click position or close if already open
      if (this.showMenu) {
        this.showMenu = false; // Close menu when clicking outside of the items
      } else {
        this.showMenu = true;
        this.menuPosition = { x: e.clientX, y: e.clientY }; // Open menu at the click position
      }
    },
    selectItem(item) {
      // Display an alert when a menu item is clicked
      alert(`You selected: ${item}`);
    },
    getItemPosition(index) {
      const totalItems = this.menuItems.length;  // Total number of menu items
      const angle = (index / totalItems) * (2 * Math.PI); // Calculate angle in radians
      const radius = 90; // Distance from the center (radius of the circle)
      
      // Calculate x and y positions using cosine and sine
      const x = Math.cos(angle) * radius;
      const y = Math.sin(angle) * radius;

      // Return the style object with calculated positions
      return {
        top: `${y - 40}px`,  // Adjust to center the item (40px is half of the item size)
        left: `${x - 40}px`,
      };
    },
  },
};
</script>
  
<style>
body {
  height: 100vh; /* Full viewport height */
  display: flex; /* Use flexbox for centering */
  justify-content: center; /* Center horizontally */
  align-items: center; /* Center vertically */
  background-color: #f4f4f4; /* Light gray background */
}

#app {
  width: 100%; /* Full width */
  height: 100%; /* Full height */
}

.radial-menu {
  position: absolute; /* Positioned relative to the radial menu */
  display: flex; /* Use flexbox to align items */
  justify-content: center; /* Center content horizontally */
  align-items: center; /* Center content vertically */
}

.menu-item {
  position: absolute; /* Each item is positioned absolutely within the menu */
  width: 70px; /* Set width of each item */
  height: 70px; /* Set height of each item */
  background-color: rgb(196, 230, 247); /* Light blue background */
  border-radius: 50%; /* Make items circular */
  display: flex; /* Use flexbox for centering text */
  justify-content: center; /* Center text horizontally */
  align-items: center; /* Center text vertically */
  cursor: pointer; /* Show pointer on hover */
  transition: background-color 0.3s ease; /* Smooth color transition */
}

.menu-item:hover {
  background-color: rgb(80, 196, 242); /* Darker blue on hover */
  border: 3px solid rgb(21, 15, 142); /* Add a darker border on hover */
}
</style>

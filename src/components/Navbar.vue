<template>
  <nav>
    <ul>
      <li :class="{ active: activePage === 'home' }" @click="changePage('home')">Home</li>
      <li :class="{ active: activePage === 'outdoor' }" @click="changePage('outdoor')">Outdoor-Planer</li>
      <li :class="{ active: activePage === 'about' }" @click="changePage('about')">About Us</li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'Navbar-one',
  data() {
    return {
      activePage: 'home'
    }
  },
  methods: {
    changePage(page) {
      this.activePage = page;
      this.$emit('change-page', page);
    }
  }
}
</script>

<style scoped>
nav {
  background-color: #f0f0f0;
  padding: 10px;
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  z-index: 999;
}

ul {
  list-style-type: none;
  display: flex;
  justify-content: space-around;
  margin: 0;
  padding: 0;
}

li {
  cursor: pointer;
}

li.active {
  font-weight: bold;
}
</style>
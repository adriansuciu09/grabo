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
  padding: 10px;
  margin: 27px auto 0;
  position: relative;
  width: 600px;
  height: 50px;
  background-color: #0d519d;
  border-radius: 15px;
}

ul {
  display: flex;
  margin: 0;
  padding: 0;
}

li {
  border-right: 2px solid white;
  border-left: 2px solid white;
  line-height: 50px;
  width: 200px;
  height: 100%;
  font-size: 18px;
  display: inline-block;
  position: relative;
  text-transform: uppercase;
  text-align: center;
  color: white;
  cursor: pointer;
}

li.active {
  color: #59c0f8;
  font-weight: bold;
}

</style>
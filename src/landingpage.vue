<template>
  <div id="app">
    <h1>Welcome to Vue.js</h1>
    <button @click="toggleMessage">Toggle Message</button>
    <p v-if="showMessage">Hello, Vue.js!</p>

    <!-- Link to Admin Page -->
    <router-link
      :to="{ name: 'catfoods.index' }"
      class="nav-link text-white px-3 py-2 d-flex align-items-center"
      exact-active-class="active"
    >
      <i class="fas fa-cat me-2"></i>
      <span>Edit Menu Cat Foods</span>
    </router-link>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showMessage: false,
    };
  },
  methods: {
    toggleMessage() {
      this.showMessage = !this.showMessage;
    },
  },
};
</script>

<style scoped>
button {
  padding: 10px 20px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

button:hover {
  background-color: #367c5c;
}

p {
  font-size: 1.5em;
  margin-top: 20px;
}

router-link {
  margin-top: 20px;
  display: inline-block;
  color: #42b983;
  text-decoration: none;
}

router-link:hover {
  color: #367c5c;
}
</style>

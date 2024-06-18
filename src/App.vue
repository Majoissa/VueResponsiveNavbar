<template>
  <div id="app">
    <NavBarComponent />
    <main>
      <h1>Welcome to the website</h1>
    </main>
  </div>
</template>

<script setup>
import NavBarComponent from './components/NavBarComponent.vue';
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

main {
  padding: 20px;
}
</style>

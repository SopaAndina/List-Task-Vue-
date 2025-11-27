<template>

    <nav>
      <router-link to="/">Inicio</router-link> |
      <router-link to="/tareas">Tareas</router-link> |
      <router-link to="/about">Acerca de</router-link>
    </nav>
    <router-view />

</template>

<script setup>

import TodoList from './components/TodoList.vue';
import router from './router';



</script>

<style scoped>
nav {
  margin-bottom: 1rem;
}

nav a {
  color: #42b883;
  text-decoration: none;
  margin: 0 0.5rem;
}

nav a.router-link-active {
  font-weight: bold;
}

h1 {
  color: #ffffff;
  font-family: Arial, Helvetica, sans-serif;
  font-size: 2.5rem;
  font-weight: 600;
  text-align: center;
}
</style>

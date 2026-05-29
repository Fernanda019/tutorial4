<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <header>
    <div class="wrapper">
      <nav class="navbar">
        <RouterLink class="link--navbar" to="/">Libros</RouterLink>
        <RouterLink class="link--navbar" to="/nuevoLibro">Nuevo Libro</RouterLink>
      </nav>
    </div>
  </header>

  <RouterView />
</template>

<style scoped>

  .navbar {
    background-color: #000000;
    margin: 10px auto;
    width: 400px;
    display: flex;
    justify-content: space-around;
    border-radius: 5px;
  }

  .link--navbar {
    text-decoration: none;
    padding: 10px;
    font-weight: 700;
    font-size: 1.3rem;
    color:#000000;
    transition: color 0.3s ease-in-out;
  }

  .link--navbar:hover {
    color: #000000;
  }
</style>

<script setup>
import { RouterLink, RouterView } from 'vue-router'
</script>

<template>
  <div class="app-container">
    <nav class="navigation">
      <div class="links">
        <RouterLink class="nav-link" to="/">Bolt</RouterLink>
        <RouterLink class="nav-link" to="/kosar">Kosár</RouterLink>
        <RouterLink class="nav-link" to="/ujtermek">Új termék</RouterLink>
      </div>
    </nav>
    <RouterView />
  </div>
</template>

<style scoped>

.navigation {
  background-color: rgb(65, 65, 65); 
  padding: 10px;
}

.links {
  text-align: center; 
}

.nav-link {
  background-color: transparent;
  border: none;
  color: inherit; 
  text-decoration: none; 
  padding: 10px 20px;
  cursor: pointer;
  transition: border-radius 0.3s;
}

.nav-link:hover {
  color: #ccc;
  background-color:rgb(66, 15, 54)
  
  }
</style>

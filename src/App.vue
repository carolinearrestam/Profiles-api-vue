<script setup lang="ts">
import UserList from './components/UserList.vue'
</script>

<template>
  <div class="greeting">
    <h1>say hi to</h1>
    <h2>The Vendre Team👋🏻</h2>
  </div>
  <main class="container">
    <UserList />
  </main>
</template>

<style scoped>
.greeting {
  text-align: center;
  font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  margin: 0.5rem;
}

h1 {
  color: rgb(167, 93, 236);
  font-weight: 800;
  text-transform: uppercase;
  text-shadow: 1px 1px 3px;
}

h2 {
  font-size: 2.2rem;
  font-weight: 600;
  color: #444;
}

.container {
  max-width: 900px;
  margin: auto;
  padding: 2rem;
}
</style>

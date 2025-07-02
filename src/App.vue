<script setup lang="ts">
import UserList from './components/UserList.vue'
</script>

<template>
  <h1>Say hi to the Vendre Team👋🏻</h1>
  <main class="container">
    <UserList />
  </main>
</template>

<style>
.container {
  max-width: 1200px;
  margin: auto;
  padding: 2rem;
}

h1 {
  display: flex;
  justify-content: center;
  color: black;
  font-weight: bold;
}
</style>

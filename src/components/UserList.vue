<template>
  <div>
    <div v-if="loading">Laddar...</div>
    <div v-else class="users">
      <div v-for="user in users" :key="user.id" class="user-card">
        <img :src="user.image" :alt="user.firstName" class="avatar" />
        <h3>{{ user.firstName }} {{ user.lastName }}</h3>
        <a :href="`mailto:${user.email}`">{{ user.email }}</a>
      </div>
    </div>

    <div class="pagination">
      <button @click="prevPage" :disabled="page === 1">Föregående</button>
      <button @click="nextPage">Nästa</button>
    </div>
  </div>
</template>

<script lang="ts" setup>
import { ref, onMounted, watch } from 'vue'

interface User {
  id: number
  firstName: string
  lastName: string
  email: string
  image: string
}

const users = ref<User[]>([])
const page = ref(1)
const limit = 6
const loading = ref(true)

const fetchUsers = async () => {
  loading.value = true
  const skip = (page.value - 1) * limit
  const res = await fetch(`https://dummyjson.com/users?limit=${limit}&skip=${skip}`)
  const data = await res.json()
  users.value = data.users
  loading.value = false
}

const nextPage = () => {
  page.value++
}
const prevPage = () => {
  if (page.value > 1) page.value--
}

onMounted(fetchUsers)
watch(page, fetchUsers)
</script>

<style scoped>
.users {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 2rem;
}

.user-card {
  padding: 1rem;
  border: 1px solid #ddd;
  border-radius: 12px;
  text-align: center;
  max-width: 100%;
  word-wrap: break-word;
  background-color: #f9f9f9;
  box-shadow: 0 0 6px rgba(0, 0, 0, 0.05);
}

.avatar {
  width: 80px;
  height: 80px;
  object-fit: cover;
  border-radius: 50%;
  margin-bottom: 0.5rem;
}

.user-card h3 {
  margin: 0.5rem 0 0.25rem;
  font-size: 1.1rem;
}

.user-card a {
  display: inline-block;
  font-size: 0.9rem;
  color: #2c3e50;
  word-break: break-word;
  max-width: 100%;
}

.pagination {
  margin-top: 2rem;
  display: flex;
  justify-content: center;
  gap: 1rem;
}

button {
  padding: 0.5rem 1rem;
  border-radius: 6px;
  border: none;
  background: #2c3e50;
  color: white;
  cursor: pointer;
}

button:disabled {
  background: #ccc;
  cursor: not-allowed;
}

@media (max-width: 600px) {
  .users {
    grid-template-columns: 1fr;
    gap: 1rem;
  }

  .avatar {
    width: 60px;
    height: 60px;
  }

  .user-card {
    padding: 0.75rem;
  }

  button {
    padding: 0.5rem;
    font-size: 0.9rem;
  }
}

@media (min-width: 1024px) {
  .users {
    grid-template-columns: repeat(3, 1fr);
    gap: 2.5rem;
  }

  .user-card {
    padding: 2rem;
  }

  .avatar {
    width: 100px;
    height: 100px;
  }

  .user-card h3 {
    font-size: 1.4rem;
  }

  .user-card a {
    font-size: 1.05rem;
  }
}
</style>

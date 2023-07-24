<script setup lang="ts">
import axios from 'axios'
import { ref } from 'vue'
import { onMounted } from 'vue'

let todolist: any = ref([])
const API_URL = 'http://localhost:3000/api/v1/todolists'

const fetchData = async () => {
  await axios
    .get(API_URL)
    .then((res) => {
      todolist.value = res.data
    })
    .catch((error) => {
      console.error(error)
    })
}

onMounted(fetchData)
</script>

<template>
  <ul>
    <li v-for="todo in todolist" :key="todo.id">
      <h2>{{ todo.title }}</h2>
      <p>{{ todo.body }}</p>
    </li>
  </ul>
</template>

<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>

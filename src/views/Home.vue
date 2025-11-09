<template>
  <div class="home">
    <h1>Welcome to My Vue App</h1>
    <p>Count: {{ counter.count }}</p>
    <button @click="counter.increment">Increment</button>

    <div v-if="posts.length">
      <h2>Posts</h2>
      <ul>
        <li v-for="post in posts" :key="post.id">{{ post.title }}</li>
      </ul>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import { useCounterStore } from '../stores/counter'
import axios from 'axios'

const counter = useCounterStore()
const posts = ref([])

onMounted(async () => {
  try {
    const response = await axios.get('https://jsonplaceholder.typicode.com/posts?_limit=5')
    posts.value = response.data
  } catch (error) {
    console.error('Failed to fetch posts:', error)
  }
})
</script>

<style scoped>
.home {
  padding: 2rem;
}
button {
  margin-top: 1rem;
}
</style>
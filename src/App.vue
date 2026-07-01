<script setup>
import { ref } from 'vue'

const count = ref(0)
</script>

<template>
  <main class="app">
    <h1>Hello, World! 👋</h1>
    <p>This is a Vue.js app, deployed on Vercel.</p>
    <button type="button" @click="count++">
      You clicked me {{ count }} time{{ count === 1 ? '' : 's' }}
    </button>
  </main>
</template>

<style scoped>
.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  min-height: 100vh;
  gap: 1rem;
  text-align: center;
  padding: 1rem;
}

h1 {
  font-size: clamp(2rem, 6vw, 3.5rem);
  margin: 0;
}

p {
  margin: 0;
  color: #64748b;
  font-size: 1.1rem;
}

button {
  margin-top: 0.5rem;
  padding: 0.6rem 1.2rem;
  font-size: 1rem;
  color: #fff;
  background: #42b883;
  border: none;
  border-radius: 0.5rem;
  cursor: pointer;
  transition: background 0.2s ease;
}

button:hover {
  background: #369b6f;
}
</style>

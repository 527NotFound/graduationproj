<script setup lang="ts">
import TheWelcome from '../components/TheWelcome.vue'
</script>

<template>
  <main>
    <div class="view360-link">
      <router-link to="/view360" class="view360-button">
        360도 뷰어 보기
      </router-link>
    </div>
    <TheWelcome />
  </main>
</template>

<style scoped>
.view360-link {
  text-align: center;
  padding: 2rem;
}

.view360-button {
  display: inline-block;
  padding: 1rem 2rem;
  background-color: #42b883;
  color: white;
  text-decoration: none;
  border-radius: 4px;
  font-weight: bold;
  transition: background-color 0.3s;
}

.view360-button:hover {
  background-color: #3aa876;
}
</style>

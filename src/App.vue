<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'
import SetupScreen from './components/SetupScreen.vue'
import PlayScreen from './components/PlayScreen.vue'

const secretWord = ref('')
</script>

<template>
  <h1>Hangman</h1>
  <SetupScreen v-if="!secretWord" @submit="(word) => (secretWord = word)"></SetupScreen>
  <PlayScreen v-else :secret-word="secretWord" @reset="secretWord = ''"></PlayScreen>
</template>

<style scoped></style>

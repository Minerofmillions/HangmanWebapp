<script setup lang="ts">
import { ref } from 'vue'

const $emit = defineEmits<{
  (e: 'submit', word: string): void
}>()
const secretWord = ref('')
</script>

<template>
  <label>Secret Word/Phrase: <input type="password" v-model="secretWord" /></label>
  <br />
  <button @click="$emit('submit', secretWord.toLowerCase())">Start Game</button>
</template>

<style lang="css" scoped></style>

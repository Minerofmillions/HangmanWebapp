<script setup lang="ts">
defineProps<{ letter: string; goodGuess: boolean; badGuess: boolean }>()
const $emit = defineEmits<{ (e: 'guess'): void }>()
</script>

<template>
  <button
    :disabled="goodGuess || badGuess"
    @click="$emit('guess')"
    :class="{ goodGuess, badGuess }"
  >
    {{ letter.toUpperCase() }}
  </button>
</template>

<style lang="css" scoped>
.badGuess {
  background-color: crimson;
  color: white;
}
.goodGuess {
  background-color: forestgreen;
  color: white;
}
</style>

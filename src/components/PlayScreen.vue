<script setup lang="ts">
import { computed, onMounted, onUnmounted, reactive } from 'vue'
import LetterButton from './LetterButton.vue'

const props = defineProps<{ secretWord: string }>()
const $emit = defineEmits<{
  (e: 'reset'): void
}>()

const guesses = reactive<string[]>([])
const letters = 'abcdefghijklmnopqrstuvwxyz'

const displayedWord = computed(() => {
  let word = props.secretWord.slice()
  for (const letter of letters) {
    if (!guesses.includes(letter)) {
      word = word.replaceAll(letter, '_')
    }
  }
  return word.toUpperCase()
})

const goodGuesses = computed(() => guesses.filter((letter) => props.secretWord.includes(letter)))

const badGuesses = computed(() => guesses.filter((letter) => !props.secretWord.includes(letter)))

const numMistakes = computed(() => badGuesses.value.length)

const failed = computed(() => numMistakes.value == 6)
const succeeded = computed(
  () =>
    !Array.from(letters).some(
      (letter) => props.secretWord.includes(letter) && !guesses.includes(letter),
    ),
)

const handleGlobalKey = (event: KeyboardEvent) => {
  guess(event.key)
}

function guess(key: string) {
  if (letters.includes(key)) {
    guesses.push(key)
  }
}

onMounted(() => {
  window.addEventListener('keydown', handleGlobalKey)
})

onUnmounted(() => {
  window.removeEventListener('keydown', handleGlobalKey)
})
</script>

<template>
  <div v-if="failed">
    <h1>Sorry!</h1>
    <p>You failed! The correct answer was "{{ secretWord.toUpperCase() }}".</p>
    <button @click="$emit('reset')">New Game</button>
  </div>
  <div v-else-if="succeeded">
    <h1>Congratulations!</h1>
    <p>You won! It was "{{ secretWord.toUpperCase() }}".</p>
    <p v-if="numMistakes < 3">You made {{ numMistakes }} mistake(s).</p>
    <p v-else>You had {{ 6 - numMistakes }} mistake(s) left.</p>
    <button @click="$emit('reset')">New Game</button>
  </div>
  <div v-else>
    <p id="displayed-word">{{ displayedWord }}</p>
    <p>{{ numMistakes }} mistakes</p>
    <div id="letter-container">
      <LetterButton
        v-for="letter in letters"
        :key="letter"
        :letter="letter"
        :good-guess="goodGuesses.includes(letter)"
        :bad-guess="badGuesses.includes(letter)"
        @guess="guess(letter)"
      ></LetterButton>
    </div>
    <button @click="$emit('reset')">Reset Game</button>
  </div>
</template>

<style lang="css" scoped>
#letter-container {
  display: grid;
  grid-template-columns: repeat(9, auto);
  width: min(75%, 1000px);
}
#displayed-word {
  letter-spacing: 2px;
}
</style>

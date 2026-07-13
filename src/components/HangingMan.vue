<script lang="ts" setup>
defineProps<{
  numMistakes: number
}>()
</script>

<template>
  <svg width="200" height="200">
    <line x1="25" y1="175" x2="175" y2="175" stroke="black" stroke-width="2" />
    <line x1="50" y1="175" x2="50" y2="25" stroke="black" stroke-width="2" />
    <line x1="50" y1="25" x2="100" y2="25" stroke="black" stroke-width="2" />
    <line x1="100" y1="25" x2="100" y2="35" stroke="black" stroke-width="2" />
    <circle
      v-if="numMistakes >= 1"
      cx="100"
      cy="60"
      r="25"
      stroke="red"
      stroke-width="2"
      fill="none"
    />
    <line
      v-if="numMistakes >= 2"
      x1="100"
      y1="85"
      x2="100"
      y2="135"
      stroke="red"
      stroke-width="2"
    />
    <line v-if="numMistakes >= 5" x1="100" y1="85" x2="75" y2="110" stroke="red" stroke-width="2" />
    <line
      v-if="numMistakes >= 6"
      x1="100"
      y1="85"
      x2="125"
      y2="110"
      stroke="red"
      stroke-width="2"
    />
    <line
      v-if="numMistakes >= 3"
      x1="100"
      y1="135"
      x2="75"
      y2="160"
      stroke="red"
      stroke-width="2"
    />
    <line
      v-if="numMistakes >= 4"
      x1="100"
      y1="135"
      x2="125"
      y2="160"
      stroke="red"
      stroke-width="2"
    />
  </svg>
</template>

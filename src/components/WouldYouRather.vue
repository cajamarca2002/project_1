<script setup>
import { ref, watch } from 'vue'

defineProps({
  question: String,
  answer1: String,
  answer2: String,
})

const emit = defineEmits([
  'answer-select'
])

// initialization of `choice` with an empty string
const choice = ref('')

// Watch for changes in `choice` and emit the updated value to the parent
watch(choice, () => {
  emit("answer-select", choice.value)
})
</script>

<template>
  <div id="wyr">
    <h2>Make your choice</h2>

    <p>{{ question }}</p>

    <div>
      <input v-model="choice" v-bind:value="answer1" type="radio" id="answer-1">
      <label for="answer-1">{{ answer1 }}</label>

      <input v-model="choice" v-bind:value="answer2" type="radio" id="answer-2">
      <label for="answer-2">{{ answer2 }}</label>
    </div>
  </div>
</template>

<style scoped>
#wyr {
  background-color: hotpink;
  padding: 20px;
}

p {
  font-family: fantasy;
}
</style>



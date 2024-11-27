<script setup>
// Import Vue's `ref` for reactive variables
import { ref, watch } from 'vue';

// Emit the `stats-entered` event to App.vue
const emit = defineEmits(['stats-entered']);

// Reactive variables for height, weight, and error messages
const height = ref('');
const weight = ref('');
const errorMessage = ref('');

// Validation logic for inputs
function validateInputs(useMetric) {
  const maxHeight = useMetric ? 3 : 108; // Max height in meters or inches
  const maxWeight = useMetric ? 350 : 700; // Max weight in kilograms or pounds

  if (!height.value || height.value <= 0 || height.value > maxHeight) {
    errorMessage.value = `Height must be a positive number and less than ${maxHeight} ${
        useMetric ? 'meters' : 'inches'
    }.`;
    return false;
  }

  if (!weight.value || weight.value <= 0 || weight.value > maxWeight) {
    errorMessage.value = `Weight must be a positive number and less than ${maxWeight} ${
        useMetric ? 'kilograms' : 'pounds'
    }.`;
    return false;
  }

  errorMessage.value = ''; // Clear errors if validation passes
  return true;
}

// Handle the button click to emit stats to App.vue
function handleSubmit(useMetric) {
  if (validateInputs(useMetric)) {
    emit('stats-entered', { height: Number(height.value), weight: Number(weight.value) });
  }
}
</script>

<template>
  <div class="bmi-form">
    <h2>Enter your height and weight</h2>

    <!-- Input for height -->
    <div>
      <label>
        Height in {{ useMetric ? 'meters' : 'inches' }}:
        <input v-model="height" type="number" placeholder="Enter height" />
      </label>
    </div>

    <!-- Input for weight -->
    <div>
      <label>
        Weight in {{ useMetric ? 'kilograms' : 'pounds' }}:
        <input v-model="weight" type="number" placeholder="Enter weight" />
      </label>
    </div>

    <!-- Validation error message -->
    <p v-if="errorMessage" class="error">{{ errorMessage }}</p>

    <!-- Button to submit -->
    <button @click="handleSubmit(useMetric)">Calculate</button>
  </div>
</template>

<style scoped>
.bmi-form {
  border: 2px solid red;
  padding: 20px;
  border-radius: 10px;
  background-color: #f8f9fa;
}
.error {
  color: red;
  margin-top: 10px;
}
</style>


<template>
  <div id="bmi-form">
    <h2>Enter your height and weight</h2>

    <!-- Height Input -->
    <div>
      <label>
        Height in {{ useMetric ? "meters" : "inches" }}:
      </label>
      <input
          v-model="height"
          type="number"
          :placeholder="'Enter height in ' + (useMetric ? 'meters' : 'inches')"
          min="0"
      />
    </div>

    <!-- Weight Input -->
    <div>
      <label>
        Weight in {{ useMetric ? "kilograms" : "pounds" }}:
      </label>
      <input
          v-model="weight"
          type="number"
          :placeholder="'Enter weight in ' + (useMetric ? 'kilograms' : 'pounds')"
          min="0"
      />
    </div>

    <!-- Submit Button -->
    <button @click="handleSubmit">Calculate</button>
  </div>
</template>

<script setup>
// Reactive variables for height and weight inputs
import { ref } from "vue";

// Props to receive the metric toggle from App.vue
defineProps({
  useMetric: Boolean,
});

// Reactive variables for input fields
const height = ref(0);
const weight = ref(0);

// Emit event to send entered data back to App.vue
const emit = defineEmits(["stats-entered"]);

function handleSubmit() {
  // Input validation
  if (height.value <= 0 || weight.value <= 0) {
    alert("Height and weight must be positive numbers.");
    return;
  }

  // Emit the height and weight to the parent
  emit("stats-entered", {
    height: parseFloat(height.value),
    weight: parseFloat(weight.value),
  });
}
</script>

<style scoped>
/* Form container with red border */
#bmi-form {
  padding: 20px;
  border: 3px solid red; /* Red inner border */
  border-radius: 8px;
  background-color: #fff; /* White background */
}

/* Labels and inputs */
label {
  display: block;
  font-weight: bold;
  color: black; /* Black text for labels */
  margin-bottom: 5px;
}

input {
  width: 100%;
  padding: 10px;
  margin-bottom: 15px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

/* Submit button styling */
button {
  background-color: #007bff;
  color: white;
  border: none;
  padding: 10px 15px;
  border-radius: 5px;
  cursor: pointer;
  width: 100%;
}

button:hover {
  background-color: #0056b3;
}
</style>

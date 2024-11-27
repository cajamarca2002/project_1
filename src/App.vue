<template>
  <div id="app">
    <!-- Title -->
    <h1>Body Mass Index Calculator</h1>

    <!-- Toggle Button for Metric Units -->
    <div class="toggle-container">
      <label>
        <input type="checkbox" v-model="useMetric" />
        Use metric units
      </label>
    </div>

    <!-- BMI Form -->
    <div class="inner-container">
      <BodyMassIndexForm
          :useMetric="useMetric"
          @stats-entered="calculateBMI"
      />
    </div>

    <!-- BMI Result -->
    <div v-if="bmi !== null" class="bmi-result">
      <h2>BMI is: {{ bmi }}</h2>
    </div>
  </div>
</template>

<script setup>
// Import required libraries and components
import { ref } from "vue";
import BodyMassIndexForm from "./BodyMassIndexForm.vue";

// Reactive variable for toggling between metric and imperial units
const useMetric = ref(false);

// Reactive variable to store the BMI result
const bmi = ref(null);

// Function to calculate BMI based on selected units
function calculateBMI({ height, weight }) {
  if (useMetric.value) {
    bmi.value = (weight / (height * height)).toFixed(2); // Metric formula
  } else {
    bmi.value = ((weight / (height * height)) * 730).toFixed(2); // Imperial formula
  }
}
</script>

<style>
/* Outer container styling */
#app {
  font-family: Arial, sans-serif;
  text-align: center;
  padding: 20px;
  border: 3px solid blue; /* Blue outer border */
  max-width: 500px;
  margin: 0 auto;
  border-radius: 10px;
}

/* Title styling */
h1 {
  margin-bottom: 15px;
  color: black; /* Black text for title */
}

/* Toggle button styling */
.toggle-container {
  margin-bottom: 20px;
}

label {
  font-size: 16px;
  font-weight: bold;
  color: black; /* Black text for label */
}

.bmi-result {
  margin-top: 20px;
  color: black; /* Black text for result */
  font-size: 18px;
}
</style>

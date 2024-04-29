<script setup>
import {ref} from 'vue'

const passwordLength = ref(12)
const includeUppercase = ref(true)
const includeNumber = ref(true)
const includeSymbols = ref(true)
const generatedPassword = ref('')

const generatePassword = function () {
    const lowercaseChar = "abcdefghijklmnopqrstuvwxyz"
    const uppercaseChars = includeUppercase.value ? "ABCDEFGHIJKLMNOPQRSTUVWXYZ" : ""
    const numberChars = includeNumber.value ? "0123456789" : ""
    const symbolChar = includeSymbols.value ? "!@#$%^&*()_+[]{}|;:,.<>?/~`" : ""


    const allChars = lowercaseChar + uppercaseChars + numberChars + symbolChar

    let password = ''
    for (let i = 0; i < passwordLength.value; i++) {
        const randomIndex = Math.floor(Math.random() * allChars.length)
        password += allChars[randomIndex]
    }
    generatedPassword.value = password
}
</script>

<template>
    <div class="password-generator-container">
        <h2 class="password-generator-title">Password Generator</h2>
        <label for="length">Password Length</label>
        <input type="number" id="length" v-model="passwordLength" min="4" max="32">
        <br />

        <label for="includeUppercase">Include Uppercase: </label>
        <input type="checkbox" id="includeUppercase" v-model="includeUppercase">
        <br />

        <label for="includeNumber">Include Numbers: </label>
        <input type="checkbox" id="includeNumber" v-model="includeNumber">
        <br />

        <label for="includeSymbols">Include Symbols: </label>
        <input type="checkbox" id="includeSymbols" v-model="includeSymbols">
        <br />

        <button @click="generatePassword" class="generated-button">Generate Password</button>
        <div v-if="generatedPassword" class="generated-password">
        <strong>Your password :</strong>{{ generatedPassword }}</div>
    </div>
</template>

<style scoped>
/* Hide the default checkbox */
input[type="checkbox"] {
  appearance: none;
  -webkit-appearance: none;
  -moz-appearance: none;
  width: 16px;
  height: 16px;
  border: 1px solid #333;
  border-radius: 3px;
  outline: none;
  cursor: pointer;
  vertical-align: middle;
  position: relative;
  margin-right: 5px; /* Optional: Add some space between the checkbox and label */
}

/* Custom checkbox checkmark */
input[type="checkbox"]:checked::before {
  content: '✔';
  display: block;
  width: 16px;
  height: 16px;
  text-align: center;
  line-height: 16px;
  color: #333;
  position: absolute;
  top: 0;
  left: 0;
}

.password-generator-container {
  max-width: 400px;
  margin: 50px auto;
}

.password-generator-title {
  font-size: 24px;
  color: #333;
  margin-bottom: 20px;
}

input {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
}

.generate-button {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.generate-button:hover {
  background-color: #2980b9;
}

.generated-password {
  margin-top: 20px;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: #f9f9f9;
  color: #333;
}
</style>
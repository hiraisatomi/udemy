<script setup lang="ts">
import { computed, ref } from 'vue'
const inputtingName = ref<string>('')
const inputtingAge = ref<number>(0)

const emit = defineEmits(['register'])



const register = () => {
  const person = { id: Math.random(), name: inputtingName.value,  age: inputtingAge.value}
  console.log('person .. ', person)
  emit('register', person)
}

const nameLengthLimit = 15

const isValidName = computed(() => {
  if (inputtingName.value.length >= nameLengthLimit) {
    return false
  } else {
    return true
  }
})

const color = computed(() => {
  return isValidName.value ? 'white' : 'rgb(208, 98, 90)'
})

</script>

<template>
  <div class="form-container">
    <div class="input-container">
      <div class="input-colum">
        <span>name:</span>
        <input class="input name" v-model="inputtingName" />
      </div>
      <span v-if="!isValidName" class="error-message">{{ nameLengthLimit }} charactors or lsee, please.</span>
      <div class="input-colum">
        <span>age:</span>
        <input class="input" v-model="inputtingAge" type="number"/>
      </div>
    </div>
    <button :disabled="!isValidName" @click="register" class="register-button">register</button>
  </div>

</template>

<style scoped>
.form-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgba(40, 111, 165, 0.597);
  padding: 24px 0;
  width: 400px;
  margin-bottom: 12px;
  border-radius: 4px;
}

.input-colum {
  width: 200px;
  display: flex;
  justify-content: space-between;
}

input {
  width: 120px;
  margin-bottom: 8px;
}

.input.name {
  background-color: v-bind(color);
}

.input-container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 50px;
  margin-bottom: 20px;
}

.error-message {
  font-size: 12px;
  color: rgb(208, 98, 90);
}

span {
  font-size: 20px;
  font-weight: bold;
}
</style>
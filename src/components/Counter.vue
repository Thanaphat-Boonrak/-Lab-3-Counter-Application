<script setup>
import { ref } from 'vue'

const count = ref(0)
const step = ref(1)
const history = ref(null)
const isUndoDisabled = ref(true) 

const increaseMent = () => {
  history.value = count.value
  count.value = Math.min(100, count.value + step.value)
  isUndoDisabled.value = false
}

const decreaseMent = () => {
  if (count.value > 0) {
    history.value = count.value 
    count.value = Math.max(0, count.value - step.value) 
    isUndoDisabled.value = false
  }
}

const reset = () => {
  history.value = count.value
  count.value = 0 
  isUndoDisabled.value = false
}

const undo = () => {
  if (history.value !== null) {
    count.value = history.value 
    history.value = null
    isUndoDisabled.value = true 
  }
}
</script>

<template>
  <div class="card">
    <h1>Counter App</h1> [cite: 80, 104]
    <p class="subtitle">Click buttons to change the number</p> [cite: 105]

    <div class="count">{{ count }}</div> [cite: 81, 106]

    <div class="row">
      <button class="btn inc" @click="increaseMent">+ Increase</button> [cite: 82, 107]
      <button class="btn dec" :disabled="count === 0" @click="decreaseMent">- Decrease</button> [cite: 82, 107]
    </div>

    <div class="row">
      <button class="btn reset" @click="reset">Reset</button> [cite: 82, 108]
      <button class="btn undo" :disabled="isUndoDisabled" @click="undo" >
        Undo
      </button> [cite: 125]
    </div>

    <div class="hint">
      Step:
      <input type="number" min="1" v-model.number="step" /> [cite: 83, 109]
    </div>
  </div>
</template>

<style scoped>
button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
  filter: grayscale(1);
}

.card {
  width: min(420px, 92vw);
  background-color: white;
  border-radius: 16px;
  padding: 24px;
  margin: 10% auto;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.08);
  text-align: center;
}
</style>
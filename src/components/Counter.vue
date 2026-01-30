<script setup>
import { ref } from 'vue'

const count = ref(0)
const step = ref(1)
const history = ref(0)
const isDisible = ref(false)


const increaseMent = () => {
  count.value = Math.min(100, count.value + step.value)
  isDisible.value = true
}

const decreaseMent = () => {
  count.value = Math.max(0, count.value - step.value)
}

const reset = () => {
  history.value = count.value
  count.value = 0
  isDisible.value = false
}

const undo = () => {
  count.value = history.value
}
</script>



<template>
  <div class="card">
    <h1>Counter App</h1>
    <p class="subtitle">Click buttons to change the number</p>

    <div class="count">{{ count }}</div>

    <div class="row">
      <button class="btn inc" @click="increaseMent">+ Increase</button>
      <button class="btn dec" @click="decreaseMent">- Decrease</button>
    </div>

    <div class="row">
      <button class="btn reset" @click="reset">Reset</button>
      <button class="btn undo" :disabled="isDisible" @click="undo" >
        Undo
      </button>
    </div>

    <div class="hint">
      Step:
      <input type="number" min="1" v-model.number="step" />
    </div>
  </div>
</template>


<style scoped>
.card {
  
  width: min(420px, 92vw);
  background-color: white;
  border-radius: 16px;
  padding: 24px;
  margin: 10% auto;
  box-shadow: 0 8px 30px rgba(0, 0, 0, 0.08);
  text-align: center;
}

h1 {
  margin: 0;
  font-size: 36px;
}

.subtitle {
  color: #666;
  margin-bottom: 16px;
}

.count {
  font-size: 64px;
  font-weight: bold;
  margin: 20px 0;
}

.row {
  display: flex;
  justify-content: center;
  gap: 12px;
  margin-bottom: 12px;
}

.btn {
  padding: 10px 16px;
  border-radius: 8px;
  border: none;
  font-size: 14px;
  cursor: pointer;
}

.btn.inc {
  background: #4caf50;
  color: white;
}

.btn.dec {
  background: #f44336;
  color: white;
}

.btn.reset {
  background: #607d8b;
  color: white;
}

.btn.undo {
  background: #ff9800;
  color: white;
}


.hint {
  margin-top: 12px;
  font-size: 14px;
}

</style>

<script setup lang="ts">
import { computed } from 'vue'
import { ref, onUpdated, reactive, watch } from 'vue'

// const show = ref(false)
const inputValue = ref(0)
// const valueTimesTwo = computed(() => inputValue.value * 2)
const valueTimesTwo = computed({
  get() {
    return inputValue.value * 2
  },
  set(val) {
    inputValue.value = val / 2
  }
})

const countRef = ref(0)
const handleCountRef = () => {
  countRef.value += 1
}
watch(countRef, (newValue, oldValue) => {
  console.log(`Watch countRef from ${oldValue} to ${newValue}`)
})

const countObj = ref({ count: 0 })
const handleCountObj = () => {
  const { value: prev } = countObj
  prev.count += 1
}
watch(
  countObj,
  (newValue, oldValue) => {
    console.log(`Watch countObj from ${oldValue} to ${newValue}`)
  },
  { deep: true }
)

const countReactive = reactive({ count: 0 })
const handleCountReactive = () => {
  countReactive.count += 1
}
watch(countReactive, (newValue, oldValue) => {
  console.log(`Watch countReactive from ${oldValue} to ${newValue}`)
})

onUpdated(() => {
  console.log('Update countRef', countRef.value)
  console.log('Update countObj', countObj.value)
  console.log('Update countReactive', countReactive.count)
})
</script>

<template>
  <!-- <button @click="show = !show">{{ show ? 'Hide' : 'Show' }}</button>
  <p v-if="show">Here I am</p> -->
  <!-- <h1>{{ count.count }}</h1> -->
  <!-- <slot><h6>Nothing to see here</h6></slot> -->
  <slot name="header"><h6>Nothing to see here</h6></slot>
  <!-- <slot><h6>Hehe</h6></slot> -->
  <div class="container">
    <h1>A cookie costs $2</h1>
    <label>Cookie</label><input v-model="inputValue" /> <label>Price $</label
    ><input v-model="valueTimesTwo" />
  </div>
  <div class="container">
    <h1>Ref Primitive</h1>
    <h1>{{ countRef }}</h1>
    <button @click="handleCountRef">+1</button>
  </div>
  <div class="container">
    <h1>Ref Object</h1>
    <h1>{{ countObj }}</h1>
    <button @click="handleCountObj">+1</button>
  </div>
  <div class="container">
    <h1>Reactive</h1>
    <h1>{{ countReactive }}</h1>
    <button @click="handleCountReactive">+1</button>
  </div>
</template>

<style scoped>
.container {
  padding: 10px;
  border-bottom: red 5px solid;
}
</style>

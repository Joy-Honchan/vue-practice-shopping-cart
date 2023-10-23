<script setup lang="ts">
import { ref } from 'vue'

const show = ref(false)
</script>

<template>
  <button @click="show = !show">{{ show ? 'Hide' : 'Show' }}</button>
  <p v-if="show">Here I am</p>
</template>

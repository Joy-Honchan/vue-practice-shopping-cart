<script setup lang="ts">
import { computed, reactive } from 'vue'
import Navbar from './components/Navbar.vue'
import products from './data/Products.json'
import { ProductType } from './data/type.ts'

import Home from './components/Home/Home.vue'

const itemData = reactive<ProductType[]>(products)
const cartItems = computed(() => {
  return itemData.filter((item) => item.status === 0)
})

const handleRemoveItem = (id: number) => {
  const removeItem = itemData.find((item) => item.id === id)
  removeItem ? (removeItem.status = 1) : null
}
</script>

<template>
  <!-- <v-card> -->
  <v-layout class="bg-background">
    <Navbar :cartItems="cartItems" @removeItem="handleRemoveItem" />
    <v-main style="min-height: 100vh">
      <Home :itemData="itemData" />
    </v-main>
  </v-layout>
  <!-- </v-card> -->
</template>

<style scoped></style>

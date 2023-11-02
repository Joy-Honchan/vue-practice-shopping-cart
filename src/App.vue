<script setup lang="ts">
import { computed, reactive } from 'vue'
import Navbar from './components/Navbar.vue'
import products from './data/Products.json'
import { ProductType } from './data/type.ts'

const itemData = reactive<ProductType[]>(products)
const cartItems = computed(() => {
  return itemData.filter((item) => item.status === 0)
})

const handleRemoveItem = (id: number) => {
  const removeItem = itemData.find((item) => item.id === id)
  removeItem ? (removeItem.status = 1) : null
  // console.log('remove item', removeItem)
}
</script>

<template>
  <v-card>
    <v-layout>
      <Navbar :cartItems="cartItems" @removeItem="handleRemoveItem" />
      <v-main style="height: 100vh"></v-main>
    </v-layout>
  </v-card>
</template>

<style scoped></style>

<script setup lang="ts">
import { computed, reactive } from 'vue'
import Navbar from './components/Navbar.vue'
import products from './data/Products.json'
import { ProductType } from './data/type.ts'

import ItemCard from './components/ItemCard.vue'

const itemData = reactive<ProductType[]>(products)
const cartItems = computed(() => {
  return itemData.filter((item) => item.status === 0)
})

const handleRemoveItem = (id: number) => {
  const removeItem = itemData.find((item) => item.id === id)
  removeItem ? (removeItem.status = 1) : null
}

const handleAddtoCart = (id: number) => {
  const addItem = itemData.find((item) => item.id === id)
  addItem ? (addItem.status = 0) : null
}
</script>

<template>
  <v-layout class="bg-background">
    <Navbar :cartItems="cartItems" @removeItem="handleRemoveItem" />
    <v-main style="min-height: 100vh">
      <v-responsive :aspect-ratio="16 / 9" style="max-height: 550px">
        <v-card
          class="h-100 pa-4 pa-md-8"
          image="https://picsum.photos/id/20/3600"
        >
          <h1>One Man's Trash is Another Man's Treasure</h1>
          <p>Discover great second-handed items</p>
        </v-card>
      </v-responsive>

      <h2>Recommended</h2>
      <v-divider></v-divider>

      <v-container>
        <v-row>
          <ItemCard
            v-for="item in itemData"
            :key="item.id"
            :item="item"
            @addToCart="handleAddtoCart"
          />
        </v-row>
      </v-container>
    </v-main>
  </v-layout>
</template>

<style scoped></style>

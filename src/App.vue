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
  <v-app class="bg-background">
    <Navbar :cartItems="cartItems" @removeItem="handleRemoveItem" />
    <v-main style="min-height: 100vh">
      <v-responsive :aspect-ratio="16 / 9" style="max-height: 550px">
        <v-card class="h-100">
          <v-img
            cover
            lazy-src="https://picsum.photos/id/20/100"
            src="https://picsum.photos/id/20/3600"
          >
            <h1>One Man's Trash is Another Man's Treasure</h1>
            <p>Discover great second-handed items</p>
            <template v-slot:placeholder>
              <div class="d-flex align-center justify-center fill-height">
                <v-progress-circular
                  color="grey-lighten-4"
                  indeterminate
                ></v-progress-circular>
              </div>
            </template>
          </v-img>
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
  </v-app>
</template>

<style scoped></style>

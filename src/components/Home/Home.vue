<script setup lang="ts">
import ItemGrid from './ItemGrid.vue'
import { ProductType } from '../../data/type'

defineProps<{ itemData: ProductType[] }>()
</script>

<template>
  <!-- <v-responsive :aspect-ratio="16 / 9" style="max-height: 550px">
    <v-card class="h-100 pa-4 pa-md-8" image="https://picsum.photos/id/20/3600">
      <h1>One Man's Trash is Another Man's Treasure</h1>
      <p>Discover great second-handed items</p>
    </v-card></v-responsive
  > -->
  <h2>Recommended</h2>
  <v-divider></v-divider>
  <ItemGrid :itemData="itemData" />
</template>

<style></style>

<script setup lang="ts">
import { computed } from 'vue'
import { ProductType } from '../data/type'

const { item } = defineProps<{ item: ProductType }>()

const overlay = computed(() => {
  return item.status === 0
})

const emit = defineEmits<{
  (e: 'addToCart', id: number): void
}>()
</script>

<template>
  <v-col cols="12" md="6" lg="4" xl="3">
    <v-card class="h-100 d-flex flex-column">
      <v-img :src="`https://picsum.photos/id/${item.id}/300/200`" />

      <v-card-title class="text-h4 font-weight-bold">
        {{ item.name }}
      </v-card-title>

      <v-card-subtitle>{{ item.age }}</v-card-subtitle>

      <v-card-text>{{ item.description }}</v-card-text>

      <v-card-actions>
        <v-spacer></v-spacer>

        <v-btn
          color="info"
          variant="elevated"
          class="font-weight-medium"
          prepend-icon="mdi-plus"
          @click.stop="emit('addToCart', item.id)"
        >
          Add to Cart
        </v-btn>
      </v-card-actions>
      <v-overlay
        v-model="overlay"
        contained
        class="align-center justify-center"
      >
        <v-btn class="font-weight-black" color="background" variant="outlined">
          Sold Out
        </v-btn>
      </v-overlay>
    </v-card>
  </v-col>
</template>

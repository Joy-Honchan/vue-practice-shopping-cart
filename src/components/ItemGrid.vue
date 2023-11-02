<script setup lang="ts">
import { ProductType } from '../data/type'

defineProps<{ itemData: ProductType[] }>()

const emit = defineEmits<{
  (e: 'addToCart', id: number): void
}>()
</script>

<template>
  <v-container>
    <v-row>
      <v-col
        v-for="item in itemData"
        :key="item.id"
        cols="12"
        md="6"
        lg="4"
        xl="3"
      >
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
              variant="outlined"
              class="font-weight-medium"
              prepend-icon="mdi-cart-plus"
              @click.stop="emit('addToCart', item.id)"
            >
              <template v-slot:prepend>
                <v-icon color="primary"></v-icon>
              </template>
              Add to Cart
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

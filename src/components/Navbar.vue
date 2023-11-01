<script setup lang="ts">
import { ref, reactive } from 'vue'
import products from '../data/Products.json'
import { ProductType } from '../data/type.ts'

defineProps<{ title: string }>()

type ItemType = ProductType & {
  count: number
}

const drawer = ref(false)
const handleDrawer = () => {
  drawer.value = !drawer.value
}

const cartItems: ItemType[] = reactive(
  products.map((item) => ({
    ...item,
    count: 0
  }))
)
</script>

<template>
  <v-app-bar color="info" prominent>
    <v-toolbar-title class="text-h5">{{ title }}</v-toolbar-title>

    <v-btn>Home</v-btn>
    <v-btn>Products</v-btn>
    <v-btn>Purchase</v-btn>

    <v-spacer></v-spacer>

    <v-btn
      variant="text"
      @click.stop="handleDrawer"
      icon="mdi-cart-outline"
    ></v-btn>
  </v-app-bar>

  <v-navigation-drawer v-model="drawer" location="right" temporary>
    <v-list>
      <v-list-item
        class="my-2"
        prepend-avatar="https://randomuser.me/api/portraits/men/78.jpg"
        title="John Doe"
      ></v-list-item>

      <v-divider></v-divider>
      <v-list-subheader>Cart Items</v-list-subheader>
      <v-list-item
        v-for="item in cartItems"
        :key="item.id"
        :title="item.name"
        :subtitle="item.age"
      >
        <template v-slot:append>
          <v-btn
            color="grey-lighten-1"
            icon="mdi-delete"
            variant="text"
          ></v-btn>
        </template>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>

<style scoped></style>

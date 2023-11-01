<script setup lang="ts">
import { ref } from 'vue'

const drawer = ref(false)
const handleDrawer = () => {
  drawer.value = !drawer.value
}
</script>

<template>
  <v-app-bar color="info" prominent>
    <v-toolbar-title class="text-h5">Online Course</v-toolbar-title>

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
    <v-list-item
      class="my-2"
      prepend-avatar="https://randomuser.me/api/portraits/men/78.jpg"
      title="John Doe"
    ></v-list-item>

    <v-divider></v-divider>
  </v-navigation-drawer>
</template>

<style scoped></style>

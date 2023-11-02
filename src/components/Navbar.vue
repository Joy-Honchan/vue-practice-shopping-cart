<script setup lang="ts">
import { ref } from 'vue'
import { ProductType } from '../data/type.ts'

defineProps<{ cartItems: ProductType[] }>()

const emit = defineEmits<{ (e: 'removeItem', id: number): void }>()

const pressRemove = (id: number) => {
  emit('removeItem', id)
}

const drawer = ref(false)
const handleDrawer = () => {
  drawer.value = !drawer.value
}
</script>

<template>
  <v-app-bar color="info" prominent>
    <v-toolbar-title class="text-h5">Used Treasure</v-toolbar-title>

    <v-btn>Home</v-btn>
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
            @click.stop="pressRemove(item.id)"
          ></v-btn>
        </template>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>

<style scoped></style>

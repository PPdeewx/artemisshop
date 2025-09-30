<script setup>
import { defineProps } from 'vue'

import UserLayout from '@/layouts/UserLayout.vue'

import { useCartStore } from '@/stores/user/cart'

const cartStore = useCartStore()

const changeQuantity = (event, index) => {
  const newQuantity = parseInt(event.target.value)
  cartStore.updateQuantity(index, newQuantity)
}

defineProps({
  products: Array,
  addToCart: Function
})
</script>

<template>
    <section class="grid grid-cols-3 gap-8 m-4">
        <div v-for="product in products" class="card w-full bg-base-100 shadow-xl" :key="product">
          <figure>
            <RouterLink :to="''">
              <img class="w-full" :src="product.imageUrl" />
            </RouterLink>
          </figure>
          <div class="card-body">
            <h2 class="card-title">{{ product.name }}</h2>
            <p>{{ product.about }}</p>
            <div class="card-actions justify-between">
              <b class="text-info text-2xl mt-auto text-orange-400">{{ product.price }} บาท</b>
              <button class="btn btn-primary" @click="addToCart(product)">Buy Now</button>
            </div>
          </div>
        </div>
    </section>
</template>
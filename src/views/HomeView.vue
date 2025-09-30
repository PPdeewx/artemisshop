<script setup>
import { useRouter } from 'vue-router'

import UserLayout from '@/layouts/UserLayout.vue'
import Product from '@/components/Product.vue'

import { useProductStore } from '@/stores/user/product'
import { useCartStore } from '@/stores/user/cart'

const router = useRouter()
const productStore = useProductStore()
const cartStore = useCartStore()

const addToCart = (product) => {
  cartStore.addToCart(product)
  router.push({ name: 'cart' })
}
</script>

<template>
  <UserLayout>
    <div class="hero min-h-screen" style="background-image: url(https://themomentum.co/wp-content/uploads/2022/10/web-PA-Shinjuku-Outlet-1280x720.jpg);">
      <div class="hero-overlay bg-opacity-60"></div>
      <div class="hero-content text-center text-neutral-content">
        <div class="max-w-md">
          <h1 class="mb-5 text-5xl font-bold">Artemis</h1>
          <p class="mb-5">Trust your intuition!</p>
          <button class="btn btn-primary">Go Shop</button>
        </div>
      </div>
      </div>

      <Product
        :products="productStore.list"
        :addToCart="addToCart"
      ></Product>
    <div class="flex justify-center">
      <div class="join mb-5">
        <input class="join-item btn btn-square btn-active" type="radio" name="options" aria-label="1" checked />
        <RouterLink :to="{ name: 'home2' }"><input class="join-item btn btn-square" type="radio" name="options" aria-label="2" /></RouterLink>
        <RouterLink :to="{ name: 'home3' }"><input class="join-item btn btn-square" type="radio" name="options" aria-label="3" /></RouterLink>
      </div>
    </div>
  </UserLayout>
</template>

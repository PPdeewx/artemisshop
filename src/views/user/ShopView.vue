<script setup>
import { defineProps } from 'vue'
import { ref, onMounted, computed, watch } from 'vue'
import { useRoute, useRouter } from 'vue-router'
import UserLayout from '@/layouts/UserLayout.vue'

import Product from '@/components/Product.vue'

import { useProductStore } from '@/stores/user/product'
import { useCartStore } from '@/stores/user/cart'

const route = useRoute()
const router = useRouter()

console.log(route.params.id)

const productStore = useProductStore()
const cartStore = useCartStore()

const searchText = ref('')

watch(() => route.query.q, (newSearchText) => {
  searchText.value = newSearchText
}, { immediate: true })

const filterProducts = computed(() => {
  return productStore.filterProducts(searchText.value)
})

const addToCart = (product) => {
  cartStore.addToCart(product)
  router.push({ name: 'cart' })
}
</script>
<template>
  <div class="row">
    <div class="col-md-6">
        <img class="w-full" :src="product.imageUrl" />
    </div>
  </div>
</template>

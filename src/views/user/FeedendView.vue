<script setup>
import { ref, onMounted } from 'vue'
import { RouterLink, useRouter } from 'vue-router'

import { useCartStore } from '@/stores/user/cart'

const cartStore = useCartStore()

const router = useRouter()

const isLoggedIn = ref(false)
const searchText = ref('')

onMounted(() => {
  if (localStorage.getItem('isLoggedIn')) {
    isLoggedIn.value = true
  }
})

const login = () => {
  isLoggedIn.value = true
  localStorage.setItem('isLoggedIn', true)
}

const logout = () => {
  isLoggedIn.value = false
  localStorage.removeItem('isLoggedIn')
}

const handleSearch = (event) => {
  if (event.key === 'Enter') {
    router.push({
      name: 'search',
      query: {
        q: searchText.value
      }
    })
  }
}
</script>
<template>
  <UserLayout>
    <div class="navbar bg-base-100">
      <div class="flex-1">
        <RouterLink :to="{ name: 'home' }" class="btn btn-ghost text-3xl font-bold">
          A R T E M I S
        </RouterLink>
      </div>
      <div class="flex-none gap-2">
        <div class="form-control">
          <input type="text"
          placeholder="Search"
          class="input input-bordered w-24 md:w-auto"
          v-model="searchText"
          @keyup="handleSearch" />
        </div>
        <div class="dropdown dropdown-end">
          <div tabindex="0" role="button" class="btn btn-ghost btn-circle">
            <div class="indicator">
              <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor"><path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 3h2l.4 2M7 13h10l4-8H5.4M7 13L5.4 5M7 13l-2.293 2.293c-.63.63-.184 1.707.707 1.707H17m0 0a2 2 0 100 4 2 2 0 000-4zm-8 2a2 2 0 11-4 0 2 2 0 014 0z" /></svg>
              <span class="badge badge-sm indicator-item">{{ cartStore.summaryQuantity }}</span>
            </div>
          </div>
          <div tabindex="0" class="mt-3 z-[1] card card-compact dropdown-content w-52 bg-base-100 shadow">
            <div class="card-body">
              <span class="font-bold text-lg">{{ cartStore.summaryQuantity }} Items</span>
              <span class="text-info">Subtotal: {{ cartStore.summaryPrice }} B</span>
              <div class="card-actions">
                <RouterLink :to="{ name: 'cart' }" class="btn btn-primary btn-block">
                  View cart
                </RouterLink>
              </div>
            </div>
          </div>
        </div>
        <button @click="login" v-if="!isLoggedIn" class="btn btn-ghost">
          <RouterLink :to="{ name: 'login' }">Login</RouterLink>
        </button>
        <div v-else class="dropdown dropdown-end">
          <div tabindex="0" role="button" class="btn btn-ghost btn-circle avatar">
            <div class="w-10 rounded-full">
              <img alt="Tailwind CSS Navbar component" src="https://tse4.mm.bing.net/th?id=OIP.ey0rShaVNsv2AbYkoZlvcwAAAA&pid=Api&P=0&h=180" />
            </div>
          </div>
          <ul tabindex="0" class="mt-3 z-[1] p-2 shadow menu menu-sm dropdown-content bg-base-100 rounded-box w-52">
            <li>
              <RouterLink :to="{ name: 'profile' }">Profile</RouterLink>
            </li>
            <li>
              <RouterLink :to="{ name: 'order' }">Order</RouterLink>
            </li>
            <li>
              <a @click="logout">Logout</a>
            </li>
          </ul>
        </div>
      </div>
    </div>
    <div class="max-w-3xl mx-auto mt-24 flex w-full flex-col rounded-lg p-24">
      <div class="text-4xl font-bold text-center pt-20">
        <h1>THANK YOU !!</h1>
        <h1>For Your Feedback</h1>
        <img class="w-64 h-64 mx-auto" src="https://upload.wikimedia.org/wikipedia/commons/thumb/0/04/Thank-you-transparent.svg/600px-Thank-you-transparent.svg.png">
      </div>
    </div>  
  </UserLayout>
</template>

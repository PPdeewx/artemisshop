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
    <div class="mt-10 mx-auto px-5 max-w-2xl bg-base-200 bg-opacity-100">
      <br><a class="font-bold text-center text-3xl">ตรวจสอบชื่อที่อยู่เพื่อทำการจัดส่งสินค้า</a><br><br> 
        <a class="text-xl">ชื่อ : Artemis Store <br>
        ที่อยู่ : 19 หมู่ 2 ตำบลแม่กา อำเภอเมือง จังหวัดพะเยา 56000 <br>
        อีเมล : Ar*********@gmail.com <br>
        เบอร์โทรศัพท์ : 099-*****99 <br><br><br></a>
    </div>
    <div class="mt-14 mx-auto mb-14 px-5 max-w-2xl bg-base-200 bg-opacity-90">
      <br><a class="font-bold text-center text-3xl">เลือกประเภทการชำระเงิน</a><br><br>
      <input type="radio" id="option1" name="group1" checked="checked" class="checkbox checkbox-xs" /><label for="option1"><a class="px-3 text-xl">โอนเงินผ่านบัญชีธนาคาร</a></label><br><br>
      <input type="radio" id="option2" name="group1" checked="checked" class="checkbox checkbox-xs" /><label for="option2"><a class="px-3 text-xl">เก็บเงินปลายทาง</a></label><br><br>
      <p class="text-x" style="color: red;">* เมื่อได้รับสินค้าแล้ว กรุณาตรวจสอบสินค้าก่อนเซ็นรับสินค้าทุกครั้ง หากท่านเซ็นรับสินค้าแล้ว ทางเราขอสงวนสิทธิ์ในการรับผิดชอบต่อสินค้า</p>
      <RouterLink :to="{ name: 'success' }" class="btn btn-wide mt-4 bg-black text-white">CONFIRM PAYMENT</RouterLink><br><br>
    </div>
  </UserLayout>
</template>
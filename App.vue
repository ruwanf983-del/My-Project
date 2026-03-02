<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'
import type { Product } from './types/Product'
import ProductCard from './components/ProductCard.vue'

// Products array
const products = ref<Product[]>([])

// Search query
const searchQuery = ref('')

// Selected product for modal
const selectedProduct = ref<Product | null>(null)

// Fetch products from API
onMounted(async () => {
  const response = await fetch('https://dummyjson.com/products')
  const data = await response.json()
  products.value = data.products
})

// Computed filtered products based on search
const filteredProducts = computed(() => {
  return products.value.filter(product =>
    product.title.toLowerCase().includes(searchQuery.value.toLowerCase())
  )
})

// Close modal function
const closeModal = () => {
  selectedProduct.value = null
}
</script>

<template>
  <div class="p-4">
    <h1 class="text-2xl font-bold mb-4">Product List</h1>

    <!-- Search input -->
    <input
      v-model="searchQuery"
      type="text"
      placeholder="Search products..."
      class="border p-2 rounded w-full mb-4"
    />

    <!-- Product grid -->
    <div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 gap-4">
      <ProductCard
        v-for="product in filteredProducts"
        :key="product.id"
        :product="product"
        @select="selectedProduct = $event"
      />
    </div>
  </div>

  <!-- Modal for product details -->
  <div
    v-if="selectedProduct"
    class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center"
  >
    <div class="bg-white p-6 rounded w-96 relative">
      <button
        class="absolute top-2 right-2 text-red-500 text-xl font-bold"
        @click="closeModal"
      >
      <div class="p-4 bg-gradient-to-r from-purple-100 via-pink-100 to-yellow-100 min-h-screen"></div>
        ✕
      </button>

      <img
        :src="selectedProduct.thumbnail"
        class="w-full h-48 object-cover rounded mb-2"
      />

      <h2 class="text-xl font-bold mb-2">
        {{ selectedProduct.title }}
      </h2>

      <p class="mb-2 text-gray-700">
        {{ selectedProduct.description }}
      </p>

      <p class="text-green-600 font-semibold text-lg">
        ${{ selectedProduct.price }}
      </p>
    </div>
  </div>
</template>

<style>
/* Tailwind CSS already handles most styling */
</style>
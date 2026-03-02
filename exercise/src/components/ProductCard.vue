<template>
  <div 
    class="border p-4 rounded shadow hover:shadow-lg transition cursor-pointer"
    @click="emit('select', product)"
  >
    <img 
      :src="product.thumbnail" 
      class="w-full h-40 object-cover rounded mb-2"
    />
    <h2 class="font-bold text-lg">{{ product.title }}</h2>
    <p class="text-green-600 font-semibold">${{ product.price }}</p>
  </div>
</template>

<script setup lang="ts">
import type { Product } from '../types/Product'

interface Props {
  product: Product
}

defineProps<Props>()

const emit = defineEmits<{
  (e: 'select', product: Product): void
}>()
</script>
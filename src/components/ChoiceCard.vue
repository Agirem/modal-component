<template>
  <label class="relative w-full md:w-[200px]">
    <input 
      type="radio" 
      :name="name" 
      :value="value" 
      class="peer hidden"
    >
    <div class="border rounded-lg p-4 md:p-6 h-auto md:h-28 cursor-pointer peer-checked:border-black peer-checked:border-2 relative">
      <div class="absolute top-4 right-4 w-4 h-4 rounded-full border border-gray-300 peer-checked:bg-black">
        <img 
          src="../assets/icons/cocher.svg" 
          alt="coché" 
          class="absolute inset-0 w-4 h-4 opacity-0 peer-checked:opacity-100"
        >
      </div>
      <div class="flex flex-col">
        <span class="text-left font-medium mb-2">{{ title }}</span>
        <span class="text-xs text-gray-500 text-left">{{ description }}</span>
      </div>
    </div>
  </label>
</template>

<script setup>
defineProps({
  name: {
    type: String,
    required: true
  },
  value: {
    type: String,
    required: true
  },
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  }
})
</script> 
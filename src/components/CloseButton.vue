<template>
  <button 
    @click="$emit('click')"
    class="absolute right-4 top-4 h-10 rounded-full bg-gray-100 flex items-center justify-center hover:bg-gray-200"
  >
    <img src="../assets/icons/close-line.svg" alt="fermer" class="w-5 h-5">
  </button>
</template>

<script setup>
defineEmits(['click'])
</script> 
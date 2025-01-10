<template>
  <div class="flex items-center">
    <img :src="iconSrc" :alt="iconAlt" class="w-5 h-5">
    <span class="text-sm text-left mx-2" :class="{ 'font-bold': isActive }">{{ label }}</span>
    <img 
      v-if="showArrow" 
      :src="arrowIcon" 
      alt="arrow" 
      class="w-6 h-6 hidden md:block"
    >
  </div>
</template>

<script setup>
import arrowIcon from '../assets/icons/arrow-step.svg'

defineProps({
  iconSrc: {
    type: String,
    required: true
  },
  iconAlt: {
    type: String,
    required: true
  },
  label: {
    type: String,
    required: true
  },
  isActive: {
    type: Boolean,
    default: false
  },
  showArrow: {
    type: Boolean,
    default: false
  }
})
</script> 
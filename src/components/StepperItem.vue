<template>
  <div class="flex items-center">
    <svg 
      v-if="iconAlt === 'user'"
      width="12" 
      height="17" 
      viewBox="0 0 12 17" 
      class="w-5 h-5"
      :class="{ 
        'text-black dark:text-white': true,
        'opacity-100': isActive, 
        'opacity-50': !isActive 
      }"
    >
      <path 
        d="M1.5 5.25C1.5 7.73625 3.51375 9.75 6 9.75C8.48625 9.75 10.5 7.73625 10.5 5.25C10.5 2.76375 8.48625 0.75 6 0.75C3.51375 0.75 1.5 2.76375 1.5 5.25Z" 
        :fill="'currentColor'"
      />
      <path 
        d="M6 10.5C2.68629 10.5 0 13.1863 0 16.5H12C12 13.1863 9.31371 10.5 6 10.5Z" 
        :fill="'currentColor'"
      />
    </svg>
    <img 
      v-else
      :src="iconSrc" 
      :alt="iconAlt" 
      class="w-5 h-5 dark:invert" 
      :class="{ 
        'opacity-100': isActive, 
        'opacity-50': !isActive 
      }"
    >
    <span 
      class="text-sm text-left mx-2" 
      :class="{ 
        'font-bold text-black dark:text-white': isActive,
        'text-gray-500 dark:text-gray-400': !isActive 
      }"
    >
      {{ label }}
    </span>
    <img 
      v-if="showArrow" 
      :src="arrowIcon" 
      alt="arrow" 
      class="w-6 h-6 hidden md:block dark:invert dark:opacity-50"
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
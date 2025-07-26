<template>
  <div v-if="loading" class="flex justify-center items-center" :class="fullScreen ? 'min-h-64' : ''">
    <div class="flex flex-col items-center space-y-3">
      <div class="relative">
        <div class="w-10 h-10 border-4 border-primary-100 dark:border-primary-800 rounded-full animate-pulse"></div>
        <div class="absolute top-0 left-0 w-10 h-10 border-4 border-transparent border-t-primary-500 dark:border-t-primary-400 rounded-full animate-spin"></div>
      </div>
      <span v-if="text" class="text-sm font-medium text-dimmed">{{ text }}</span>
    </div>
  </div>
</template>

<script setup>
defineProps({
  loading: {
    type: Boolean,
    default: false
  },
  text: {
    type: String,
    default: ''
  },
  fullScreen: {
    type: Boolean,
    default: false
  }
})
</script> 
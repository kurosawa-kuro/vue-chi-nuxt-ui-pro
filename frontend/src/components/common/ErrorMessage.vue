<template>
  <div v-if="message" class="card border-l-4 border-l-red-500 bg-red-50/50 dark:bg-red-500/10 backdrop-blur-sm p-4">
    <div class="flex items-start">
      <div class="flex-shrink-0">
        <div class="w-8 h-8 bg-red-100 dark:bg-red-500/20 rounded-full flex items-center justify-center">
          <svg class="w-4 h-4 text-red-500 dark:text-red-400" fill="currentColor" viewBox="0 0 20 20">
            <path fill-rule="evenodd" d="M10 18a8 8 0 100-16 8 8 0 000 16zM8.707 7.293a1 1 0 00-1.414 1.414L8.586 10l-1.293 1.293a1 1 0 101.414 1.414L10 11.414l1.293 1.293a1 1 0 001.414-1.414L11.414 10l1.293-1.293a1 1 0 00-1.414-1.414L10 8.586 8.707 7.293z" clip-rule="evenodd" />
          </svg>
        </div>
      </div>
      <div class="ml-3 flex-1">
        <h3 class="text-sm font-semibold text-red-800 dark:text-red-200 mb-1">Error</h3>
        <p class="text-sm text-red-700 dark:text-red-300 leading-relaxed">{{ message }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
defineProps({
  message: {
    type: String,
    required: true
  }
})
</script> 
<template>
  <button
    @click="openSearch"
    class="flex items-center w-full p-2 text-left rounded-lg border border-gray-200 dark:border-gray-700 bg-gray-50 dark:bg-gray-800 hover:bg-gray-100 dark:hover:bg-gray-700 transition-colors group"
    :class="{ 'justify-center': collapsed }"
  >
    <SearchIcon class="h-4 w-4 text-gray-400 group-hover:text-gray-500" />
    <span 
      v-if="!collapsed"
      class="ml-3 text-sm text-gray-500 group-hover:text-gray-600 dark:text-gray-400 dark:group-hover:text-gray-300"
    >
      Search...
    </span>
    <div 
      v-if="!collapsed"
      class="ml-auto flex items-center space-x-1"
    >
      <kbd class="hidden sm:inline-block px-1.5 py-0.5 text-xs font-mono bg-white dark:bg-gray-700 border border-gray-200 dark:border-gray-600 rounded">
        ⌘
      </kbd>
      <kbd class="hidden sm:inline-block px-1.5 py-0.5 text-xs font-mono bg-white dark:bg-gray-700 border border-gray-200 dark:border-gray-600 rounded">
        K
      </kbd>
    </div>
  </button>
</template>

<script setup>
import { SearchIcon } from 'lucide-vue-next'

const props = defineProps({
  collapsed: {
    type: Boolean,
    default: false
  }
})

const openSearch = () => {
  window.dispatchEvent(new CustomEvent('open-search'))
}
</script>
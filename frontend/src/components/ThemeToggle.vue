<template>
  <button
    @click="toggleTheme"
    class="p-2 rounded-lg text-gray-500 hover:text-gray-600 hover:bg-gray-100 dark:text-gray-400 dark:hover:text-gray-300 dark:hover:bg-gray-700 transition-colors"
    :title="isDark ? 'Switch to light mode' : 'Switch to dark mode'"
  >
    <SunIcon v-if="isDark" class="h-5 w-5" />
    <MoonIcon v-else class="h-5 w-5" />
  </button>
</template>

<script setup>
import { useDark, useToggle } from "@vueuse/core"
import { SunIcon, MoonIcon } from 'lucide-vue-next'

const isDark = useDark({
  selector: 'html',
})

const toggleTheme = useToggle(isDark)
</script>

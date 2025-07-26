<template>
  <div class="dashboard-panel">
    <div class="flex h-screen overflow-hidden">
      <!-- Sidebar -->
      <Sidebar
        :sidebarOpen="sidebarOpen"
        @close-sidebar="sidebarOpen = false"
        variant="v2"
        class="dashboard-sidebar"
      />

      <!-- Content area -->
      <div class="relative flex flex-col flex-1 overflow-y-auto overflow-x-hidden bg-gray-50 dark:bg-gray-900">
        <!-- Site header -->
        <Header
          :sidebarOpen="sidebarOpen"
          @toggle-sidebar="sidebarOpen = !sidebarOpen"
          variant="v2"
          class="dashboard-navbar"
        />

        <!-- Main content -->
        <main class="flex-1 p-6">
          <div class="max-w-7xl mx-auto">
            <slot />
          </div>
        </main>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import Sidebar from '@/partials/SimpleSidebar.vue'
import Header from '@/partials/SimpleHeader.vue'

const sidebarOpen = ref(false)
</script>

<style scoped>
.dashboard-panel {
  @apply bg-gray-50 dark:bg-gray-900 min-h-screen;
}
</style> 
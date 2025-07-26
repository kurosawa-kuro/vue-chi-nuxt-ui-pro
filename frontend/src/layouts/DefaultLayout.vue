<template>
  <div class="min-h-screen bg-gray-50 dark:bg-gray-900">
    <div class="flex h-screen overflow-hidden">
      <!-- Sidebar -->
      <div class="flex">
        <ModernSidebar
          v-model:open="sidebarOpen"
          :collapsible="true"
          :resizable="true"
        />
      </div>

      <!-- Content area -->
      <div class="relative flex flex-col flex-1 overflow-y-auto overflow-x-hidden">
        <!-- Modern Header -->
        <ModernHeader
          :sidebar-open="sidebarOpen"
          @toggle-sidebar="sidebarOpen = !sidebarOpen"
        />

        <!-- Main content -->
        <main class="flex-1 p-6">
          <div class="max-w-7xl mx-auto">
            <slot />
          </div>
        </main>
      </div>
    </div>

    <!-- Search Modal -->
    <SearchModal />
    
    <!-- Notifications Slideover -->
    <NotificationsSlider />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import ModernSidebar from '@/components/layout/ModernSidebar.vue'
import ModernHeader from '@/components/layout/ModernHeader.vue'
import SearchModal from '@/components/layout/SearchModal.vue'
import NotificationsSlider from '@/components/layout/NotificationsSlider.vue'

const sidebarOpen = ref(false)
</script> 
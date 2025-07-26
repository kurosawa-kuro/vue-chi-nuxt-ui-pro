<template>
  <header class="sticky top-0 z-40 w-full border-b border-gray-200 dark:border-gray-700 bg-white/95 dark:bg-gray-900/95 backdrop-blur supports-[backdrop-filter]:bg-white/60 dark:supports-[backdrop-filter]:bg-gray-900/60">
    <div class="px-4 sm:px-6 lg:px-8">
      <div class="flex items-center justify-between h-16">

        <!-- Header: Left side -->
        <div class="flex items-center">
          <!-- Hamburger button -->
          <button 
            class="w-9 h-9 flex items-center justify-center rounded-lg text-gray-500 hover:text-gray-600 hover:bg-gray-100 dark:text-gray-400 dark:hover:text-gray-300 dark:hover:bg-gray-800 transition-colors lg:hidden" 
            @click.stop="$emit('toggle-sidebar')" 
            aria-controls="sidebar" 
            :aria-expanded="sidebarOpen"
          >
            <span class="sr-only">Open sidebar</span>
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
            </svg>
          </button>

          <!-- Logo/Brand (visible on mobile) -->
          <div class="lg:hidden ml-3">
            <router-link to="/" class="flex items-center space-x-2">
              <div class="w-8 h-8 bg-gradient-to-br from-primary-500 to-primary-600 rounded-lg flex items-center justify-center">
                <svg class="w-4 h-4 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
                </svg>
              </div>
              <span class="text-lg font-semibold text-gray-900 dark:text-white">Vue Chi</span>
            </router-link>
          </div>
        </div>

        <!-- Header: Right side -->
        <div class="flex items-center space-x-2">
          <!-- Search Button -->
          <button
            class="w-9 h-9 flex items-center justify-center rounded-lg text-gray-500 hover:text-gray-600 hover:bg-gray-100 dark:text-gray-400 dark:hover:text-gray-300 dark:hover:bg-gray-800 transition-colors"
            :class="{ 'bg-gray-100 dark:bg-gray-800 text-gray-600 dark:text-gray-300': searchModalOpen }"
            @click.stop="searchModalOpen = true"
            aria-controls="search-modal"
          >
            <span class="sr-only">Search</span>
            <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
            </svg>
          </button>
          
          <SearchModal id="search-modal" searchId="search" :modalOpen="searchModalOpen" @open-modal="searchModalOpen = true" @close-modal="searchModalOpen = false" />
          
          <!-- Notifications -->
          <Notifications align="right" />
          
          <!-- Help -->
          <Help align="right" />
          
          <!-- Theme Toggle -->
          <ThemeToggle />
          
          <!-- Divider -->
          <div class="w-px h-6 bg-gray-200 dark:bg-gray-700"></div>
          
          <!-- User Menu -->
          <UserMenu align="right" />
        </div>

      </div>
    </div>
  </header>
</template>

<script>
import { ref } from 'vue'

import SearchModal from '../components/ModalSearch.vue'
import Notifications from '../components/DropdownNotifications.vue'
import Help from '../components/DropdownHelp.vue'
import ThemeToggle from '../components/ThemeToggle.vue'
import UserMenu from '../components/DropdownProfile.vue'

export default {
  name: 'Header',
  props: [
    'sidebarOpen',
    'variant',
  ],
  components: {
    SearchModal,
    Notifications,
    Help,
    ThemeToggle,
    UserMenu,
  },
  setup() {
    const searchModalOpen = ref(false)
    return {
      searchModalOpen,
    }  
  }  
}
</script>
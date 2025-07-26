<template>
  <div class="min-w-fit">
    <!-- Sidebar backdrop (mobile only) -->
    <div 
      class="fixed inset-0 bg-gray-900/50 backdrop-blur-sm z-40 lg:hidden transition-opacity duration-200" 
      :class="sidebarOpen ? 'opacity-100' : 'opacity-0 pointer-events-none'" 
      aria-hidden="true"
      @click="$emit('close-sidebar')"
    ></div>

    <!-- Sidebar -->
    <div
      id="sidebar"
      ref="sidebar"
      class="flex lg:flex! flex-col fixed z-50 left-0 top-0 lg:static lg:left-auto lg:top-auto lg:translate-x-0 h-[100dvh] overflow-y-auto w-72 lg:w-20 lg:sidebar-expanded:!w-72 2xl:w-72! shrink-0 bg-white dark:bg-gray-900 border-r border-gray-200 dark:border-gray-700 transition-all duration-200 ease-in-out"
      :class="sidebarOpen ? 'translate-x-0' : '-translate-x-72'"
    >

      <!-- Sidebar header -->
      <div class="flex items-center justify-between p-6 border-b border-gray-200 dark:border-gray-700">
        <!-- Logo -->
        <router-link to="/" class="flex items-center space-x-3">
          <div class="w-10 h-10 bg-gradient-to-br from-primary-500 to-primary-600 rounded-xl flex items-center justify-center">
            <svg class="w-5 h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M13 10V3L4 14h7v7l9-11h-7z" />
            </svg>
          </div>
          <div class="lg:hidden lg:sidebar-expanded:block 2xl:block">
            <span class="text-xl font-bold text-gray-900 dark:text-white">Vue Chi</span>
            <p class="text-xs text-dimmed">Dashboard</p>
          </div>
        </router-link>
        
        <!-- Close button (mobile) -->
        <button
          ref="trigger"
          class="lg:hidden w-8 h-8 flex items-center justify-center rounded-lg text-gray-500 hover:text-gray-600 hover:bg-gray-100 dark:text-gray-400 dark:hover:text-gray-300 dark:hover:bg-gray-800 transition-colors"
          @click.stop="$emit('close-sidebar')"
          aria-controls="sidebar"
          :aria-expanded="sidebarOpen"
        >
          <span class="sr-only">Close sidebar</span>
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
      </div>

      <!-- Navigation -->
      <nav class="flex-1 p-6 space-y-8">
        <!-- Main Navigation -->
        <div>
          <h3 class="text-xs uppercase text-gray-500 dark:text-gray-400 font-semibold mb-4 px-3">
            <span class="hidden lg:block lg:sidebar-expanded:hidden 2xl:hidden text-center w-6">•••</span>
            <span class="lg:hidden lg:sidebar-expanded:block 2xl:block">Main Menu</span>
          </h3>
          <ul class="space-y-2">
            <!-- Home -->
            <li>
              <router-link 
                to="/" 
                class="flex items-center px-3 py-2.5 rounded-xl text-sm font-medium transition-colors"
                :class="currentRoute.fullPath === '/' 
                  ? 'bg-primary-50 dark:bg-primary-500/10 text-primary-600 dark:text-primary-400 border border-primary-200 dark:border-primary-500/20' 
                  : 'text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-800 hover:text-gray-900 dark:hover:text-white'"
              >
                <div class="w-5 h-5 mr-3 flex-shrink-0">
                  <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
                  </svg>
                </div>
                <span class="lg:hidden lg:sidebar-expanded:block 2xl:block">Dashboard</span>
              </router-link>
            </li>
            
            <!-- Hello World -->
            <li>
              <router-link 
                to="/hello-world" 
                class="flex items-center px-3 py-2.5 rounded-xl text-sm font-medium transition-colors"
                :class="currentRoute.fullPath === '/hello-world' 
                  ? 'bg-primary-50 dark:bg-primary-500/10 text-primary-600 dark:text-primary-400 border border-primary-200 dark:border-primary-500/20' 
                  : 'text-gray-700 dark:text-gray-300 hover:bg-gray-100 dark:hover:bg-gray-800 hover:text-gray-900 dark:hover:text-white'"
              >
                <div class="w-5 h-5 mr-3 flex-shrink-0">
                  <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M8 12h.01M12 12h.01M16 12h.01M21 12c0 4.418-4.03 8-9 8a9.863 9.863 0 01-4.255-.949L3 20l1.395-3.72C3.512 15.042 3 13.574 3 12c0-4.418 4.03-8 9-8s9 3.582 9 8z" />
                  </svg>
                </div>
                <span class="lg:hidden lg:sidebar-expanded:block 2xl:block">Hello World</span>
              </router-link>
            </li>
          </ul>
        </div>
      </nav>

      <!-- Sidebar footer -->
      <div class="p-6 border-t border-gray-200 dark:border-gray-700">
        <div class="bg-gradient-to-r from-primary-500 to-primary-600 rounded-xl p-4 text-white">
          <div class="lg:hidden lg:sidebar-expanded:block 2xl:block">
            <h4 class="font-semibold text-sm mb-1">Vue Chi Pro</h4>
            <p class="text-xs text-white/80 mb-3">Upgrade to unlock more features</p>
            <button class="w-full bg-white/20 hover:bg-white/30 text-white text-xs font-medium py-2 px-3 rounded-lg transition-colors">
              Upgrade Now
            </button>
          </div>
          <div class="hidden lg:block lg:sidebar-expanded:hidden 2xl:hidden text-center">
            <svg class="w-6 h-6 mx-auto" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M12 8v13m0-13V6a2 2 0 112 2h-2zm0 0V5.5A2.5 2.5 0 109.5 8H12z" />
            </svg>
          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import { useRoute } from 'vue-router'
import { computed } from 'vue'

export default {
  name: 'Sidebar',
  props: [
    'sidebarOpen',
    'variant',
  ],
  emits: ['close-sidebar'],
  setup() {
    const route = useRoute()
    const currentRoute = computed(() => route)
    
    return {
      currentRoute,
    }
  }
}
</script>
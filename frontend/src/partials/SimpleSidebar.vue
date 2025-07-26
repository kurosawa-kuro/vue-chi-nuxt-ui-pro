<template>
  <div class="min-w-fit">
    <!-- Sidebar backdrop (mobile only) -->
    <div class="fixed inset-0 bg-gray-900/50 backdrop-blur-sm z-40 lg:hidden transition-opacity duration-200" :class="props.sidebarOpen ? 'opacity-100' : 'opacity-0 pointer-events-none'" aria-hidden="true" @click="$emit('close-sidebar')"></div>

    <!-- Sidebar -->
    <div
      id="sidebar"
      ref="sidebar"
      class="flex lg:flex! flex-col fixed z-50 left-0 top-0 lg:static lg:left-auto lg:top-auto lg:translate-x-0 h-[100dvh] overflow-y-auto w-72 lg:w-20 lg:sidebar-expanded:!w-72 2xl:w-72! shrink-0 bg-white dark:bg-gray-900 border-r border-gray-200 dark:border-gray-700 transition-all duration-200 ease-in-out"
      :class="props.sidebarOpen ? 'translate-x-0' : '-translate-x-72'"
    >

      <!-- Sidebar header -->
      <div class="flex items-center justify-between p-6 border-b border-gray-200 dark:border-gray-700">
        <!-- Close button -->
        <button
          ref="trigger"
          class="lg:hidden w-8 h-8 flex items-center justify-center rounded-lg text-gray-500 hover:text-gray-600 hover:bg-gray-100 dark:text-gray-400 dark:hover:text-gray-300 dark:hover:bg-gray-800 transition-colors"
          @click.stop="$emit('close-sidebar')"
          aria-controls="sidebar"
          :aria-expanded="props.sidebarOpen"
        >
          <span class="sr-only">Close sidebar</span>
          <svg class="w-5 h-5" fill="none" stroke="currentColor" viewBox="0 0 24 24">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
          </svg>
        </button>
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
      </div>

      <!-- Links -->
      <div class="space-y-8">
        <!-- Pages group -->
        <div>
          <h3 class="text-xs uppercase text-gray-400 dark:text-gray-500 font-semibold pl-3">
            <span class="hidden lg:block lg:sidebar-expanded:hidden 2xl:hidden text-center w-6" aria-hidden="true">•••</span>
            <span class="lg:hidden lg:sidebar-expanded:block 2xl:block">Pages</span>
          </h3>
          <ul class="mt-3">
            <!-- Home -->
            <li class="px-3 py-2 rounded-lg mb-0.5 last:mb-0" :class="currentRoute.fullPath === '/' && 'bg-violet-500'">
              <router-link class="block text-gray-800 dark:text-gray-100 truncate transition" :class="currentRoute.fullPath === '/' ? 'text-white' : 'hover:text-gray-900 dark:hover:text-white'" to="/">
                <div class="flex items-center">
                  <svg class="shrink-0 fill-current mr-3" :class="currentRoute.fullPath === '/' ? 'text-violet-200' : 'text-gray-400 dark:text-gray-500'" width="16" height="16" viewBox="0 0 16 16">
                    <path d="M8.707 1.293a1 1 0 0 0-1.414 0L2 6.586V15a1 1 0 0 0 1 1h10a1 1 0 0 0 1-1V6.586l-5.293-5.293Z" />
                  </svg>
                  <span class="text-sm font-medium ml-4 lg:opacity-0 lg:sidebar-expanded:opacity-100 2xl:opacity-100 duration-200">Home</span>
                </div>
              </router-link>
            </li>
            <!-- Hello World -->
            <li class="px-3 py-2 rounded-lg mb-0.5 last:mb-0" :class="currentRoute.fullPath === '/hello-world' && 'bg-violet-500'">
              <router-link class="block text-gray-800 dark:text-gray-100 truncate transition" :class="currentRoute.fullPath === '/hello-world' ? 'text-white' : 'hover:text-gray-900 dark:hover:text-white'" to="/hello-world">
                <div class="flex items-center">
                  <svg class="shrink-0 fill-current mr-3" :class="currentRoute.fullPath === '/hello-world' ? 'text-violet-200' : 'text-gray-400 dark:text-gray-500'" width="16" height="16" viewBox="0 0 16 16">
                    <path d="M8 0C3.6 0 0 3.6 0 8s3.6 8 8 8 8-3.6 8-8-3.6-8-8-8ZM8 12c-.6 0-1-.4-1-1s.4-1 1-1 1 .4 1 1-.4 1-1 1Zm1-3H7V4h2v5Z" />
                  </svg>
                  <span class="text-sm font-medium ml-4 lg:opacity-0 lg:sidebar-expanded:opacity-100 2xl:opacity-100 duration-200">Hello World</span>
                </div>
              </router-link>
            </li>
          </ul>
        </div>
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { useRoute } from 'vue-router'

const props = defineProps({
  sidebarOpen: Boolean,
  variant: String
})

const emit = defineEmits(['close-sidebar'])

const trigger = ref(null)
const sidebar = ref(null)
const sidebarExpanded = ref(localStorage.getItem('sidebar-expanded') == 'true')

const currentRoute = computed(() => useRoute())

const clickHandler = ({ target }) => {
  if (!sidebar.value || !trigger.value) return
  if (!props.sidebarOpen || sidebar.value.contains(target) || trigger.value.contains(target)) return
  emit('close-sidebar')
}

const keyHandler = ({ keyCode }) => {
  if (!props.sidebarOpen || keyCode !== 27) return
  emit('close-sidebar')
}

onMounted(() => {
  document.addEventListener('click', clickHandler)
  document.addEventListener('keydown', keyHandler)
})

onUnmounted(() => {
  document.removeEventListener('click', clickHandler)
  document.removeEventListener('keydown', keyHandler)
})

const handleSidebarToggle = () => {
  sidebarExpanded.value = !sidebarExpanded.value
  localStorage.setItem('sidebar-expanded', sidebarExpanded.value)
  if (sidebarExpanded.value) {
    document.querySelector('body').classList.add('sidebar-expanded')
  } else {
    document.querySelector('body').classList.remove('sidebar-expanded')
  }
}

onMounted(() => {
  if (sidebarExpanded.value) {
    document.querySelector('body').classList.add('sidebar-expanded')
  } else {
    document.querySelector('body').classList.remove('sidebar-expanded')
  }
})
</script>
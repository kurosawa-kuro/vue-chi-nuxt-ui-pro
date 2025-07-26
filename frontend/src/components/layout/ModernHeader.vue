<template>
  <header class="sticky top-0 z-30 bg-white/90 dark:bg-gray-800/90 backdrop-blur-md border-b border-gray-200 dark:border-gray-700">
    <div class="flex items-center justify-between h-16 px-4 sm:px-6 lg:px-8">
      <!-- Left side -->
      <div class="flex items-center">
        <!-- Mobile menu button -->
        <button
          @click="$emit('toggle-sidebar')"
          class="lg:hidden p-2 rounded-lg text-gray-500 hover:text-gray-600 hover:bg-gray-100 dark:hover:bg-gray-700"
        >
          <MenuIcon class="h-6 w-6" />
        </button>
      </div>

      <!-- Right side -->
      <div class="flex items-center space-x-3">
        <!-- Search button -->
        <button
          @click="openSearch"
          class="p-2 rounded-lg text-gray-500 hover:text-gray-600 hover:bg-gray-100 dark:hover:bg-gray-700 transition-colors"
        >
          <SearchIcon class="h-5 w-5" />
        </button>

        <!-- Notifications -->
        <Dropdown
          :items="notificationItems"
          align="right"
          width="w-80"
          trigger-class="p-2 rounded-lg text-gray-500 hover:text-gray-600 hover:bg-gray-100 dark:hover:bg-gray-700 transition-colors relative"
        >
          <template #trigger>
            <BellIcon class="h-5 w-5" />
            <span
              v-if="unreadCount > 0"
              class="absolute -top-1 -right-1 h-4 w-4 bg-red-500 text-white text-xs rounded-full flex items-center justify-center"
            >
              {{ unreadCount > 9 ? '9+' : unreadCount }}
            </span>
          </template>
        </Dropdown>

        <!-- Help -->
        <Dropdown
          :items="helpItems"
          align="right"
        >
          <template #trigger>
            <button class="p-2 rounded-lg text-gray-500 hover:text-gray-600 hover:bg-gray-100 dark:hover:bg-gray-700 transition-colors">
              <HelpCircleIcon class="h-5 w-5" />
            </button>
          </template>
        </Dropdown>

        <!-- Theme toggle -->
        <ThemeToggle />

        <!-- Divider -->
        <div class="h-6 w-px bg-gray-200 dark:bg-gray-700" />

        <!-- User menu -->
        <UserMenu />
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref, computed } from 'vue'
import { MenuIcon, SearchIcon, BellIcon, HelpCircleIcon } from 'lucide-vue-next'

import Dropdown from '@/components/ui/Dropdown.vue'
import ThemeToggle from '@/components/ThemeToggle.vue'
import UserMenu from './UserMenu.vue'

const props = defineProps({
  sidebarOpen: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['toggle-sidebar'])

const notifications = ref([
  {
    id: 1,
    title: 'New message from John',
    description: 'Hello, how are you doing?',
    time: '2 min ago',
    unread: true
  },
  {
    id: 2,
    title: 'System update',
    description: 'Your system has been updated to version 2.1',
    time: '1 hour ago',
    unread: true
  },
  {
    id: 3,
    title: 'Welcome!',
    description: 'Welcome to your new dashboard',
    time: '2 hours ago',
    unread: false
  }
])

const unreadCount = computed(() => {
  return notifications.value.filter(n => n.unread).length
})

const notificationItems = computed(() => [
  [
    {
      label: 'View all notifications',
      to: '/notifications'
    },
    {
      label: 'Mark all as read',
      onSelect: () => markAllAsRead()
    }
  ]
])

const helpItems = ref([
  [
    {
      label: 'Documentation',
      to: 'https://docs.example.com',
      target: '_blank'
    },
    {
      label: 'Contact Support',
      to: '/support'
    },
    {
      label: 'Keyboard Shortcuts',
      onSelect: () => showShortcuts()
    }
  ]
])

const openSearch = () => {
  // Emit event or use a global state to open search modal
  window.dispatchEvent(new CustomEvent('open-search'))
}

const markAllAsRead = () => {
  notifications.value.forEach(n => n.unread = false)
}

const showShortcuts = () => {
  // Show keyboard shortcuts modal
  console.log('Show shortcuts modal')
}
</script>
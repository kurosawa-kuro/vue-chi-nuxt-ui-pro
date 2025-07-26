<template>
  <Teleport to="body">
    <Transition
      enter-active-class="transition-opacity duration-300"
      enter-from-class="opacity-0"
      enter-to-class="opacity-100"
      leave-active-class="transition-opacity duration-200"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
      <div
        v-if="isOpen"
        class="fixed inset-0 z-50 overflow-hidden"
      >
        <div class="absolute inset-0 bg-gray-900/50 backdrop-blur-sm" @click="close" />
        
        <Transition
          enter-active-class="transition ease-in-out duration-300"
          enter-from-class="translate-x-full"
          enter-to-class="translate-x-0"
          leave-active-class="transition ease-in-out duration-300"
          leave-from-class="translate-x-0"
          leave-to-class="translate-x-full"
        >
          <div
            v-if="isOpen"
            class="absolute right-0 top-0 h-full w-96 bg-white dark:bg-gray-800 shadow-xl"
          >
            <!-- Header -->
            <div class="flex items-center justify-between p-6 border-b border-gray-200 dark:border-gray-700">
              <h2 class="text-lg font-semibold text-gray-900 dark:text-white">
                Notifications
              </h2>
              <div class="flex items-center space-x-2">
                <button
                  @click="markAllAsRead"
                  class="text-sm text-primary-600 hover:text-primary-700 dark:text-primary-400"
                >
                  Mark all read
                </button>
                <button
                  @click="close"
                  class="p-2 rounded-lg text-gray-400 hover:text-gray-600 hover:bg-gray-100 dark:hover:bg-gray-700"
                >
                  <XMarkIcon class="h-5 w-5" />
                </button>
              </div>
            </div>

            <!-- Notifications list -->
            <div class="flex-1 overflow-y-auto">
              <div v-if="notifications.length === 0" class="p-6 text-center">
                <BellIcon class="h-12 w-12 mx-auto text-gray-300 mb-4" />
                <p class="text-gray-500 dark:text-gray-400">No notifications</p>
              </div>

              <div v-else class="space-y-1 p-4">
                <div
                  v-for="notification in notifications"
                  :key="notification.id"
                  class="p-4 rounded-lg border transition-colors"
                  :class="notification.unread 
                    ? 'bg-primary-50 dark:bg-primary-900/20 border-primary-200 dark:border-primary-800' 
                    : 'bg-white dark:bg-gray-800 border-gray-200 dark:border-gray-700 hover:bg-gray-50 dark:hover:bg-gray-700'"
                >
                  <div class="flex">
                    <div class="flex-1">
                      <div class="flex items-start justify-between">
                        <p class="text-sm font-medium text-gray-900 dark:text-white">
                          {{ notification.title }}
                        </p>
                        <div
                          v-if="notification.unread"
                          class="ml-2 h-2 w-2 bg-primary-600 rounded-full flex-shrink-0"
                        />
                      </div>
                      <p class="mt-1 text-sm text-gray-600 dark:text-gray-300">
                        {{ notification.description }}
                      </p>
                      <p class="mt-2 text-xs text-gray-500 dark:text-gray-400">
                        {{ notification.time }}
                      </p>
                    </div>
                  </div>
                  
                  <div v-if="notification.actions" class="mt-3 flex space-x-2">
                    <button
                      v-for="action in notification.actions"
                      :key="action.label"
                      @click="handleAction(notification, action)"
                      class="text-xs px-3 py-1 rounded-lg border border-gray-200 dark:border-gray-600 hover:bg-gray-100 dark:hover:bg-gray-700 transition-colors"
                    >
                      {{ action.label }}
                    </button>
                  </div>
                </div>
              </div>
            </div>

            <!-- Footer -->
            <div class="border-t border-gray-200 dark:border-gray-700 p-4">
              <router-link
                to="/notifications"
                @click="close"
                class="block w-full text-center py-2 text-sm text-primary-600 hover:text-primary-700 dark:text-primary-400"
              >
                View all notifications
              </router-link>
            </div>
          </div>
        </Transition>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { X as XMarkIcon, Bell as BellIcon } from 'lucide-vue-next'

const isOpen = ref(false)

const notifications = ref([
  {
    id: 1,
    title: 'New message from John',
    description: 'Hello, how are you doing today? I wanted to check in.',
    time: '2 minutes ago',
    unread: true,
    actions: [
      { label: 'Reply', type: 'primary' },
      { label: 'Mark read', type: 'secondary' }
    ]
  },
  {
    id: 2,
    title: 'System update completed',
    description: 'Your system has been successfully updated to version 2.1.0',
    time: '1 hour ago',
    unread: true
  },
  {
    id: 3,
    title: 'Welcome to the platform!',
    description: 'Thank you for joining us. Here are some quick tips to get started.',
    time: '2 hours ago',
    unread: false
  }
])

const open = () => {
  isOpen.value = true
}

const close = () => {
  isOpen.value = false
}

const markAllAsRead = () => {
  notifications.value.forEach(notification => {
    notification.unread = false
  })
}

const handleAction = (notification, action) => {
  console.log('Action clicked:', action.label, 'for notification:', notification.id)
  
  if (action.type === 'secondary' && action.label === 'Mark read') {
    notification.unread = false
  }
}

const handleOpenNotifications = () => {
  open()
}

onMounted(() => {
  window.addEventListener('open-notifications', handleOpenNotifications)
})

onUnmounted(() => {
  window.removeEventListener('open-notifications', handleOpenNotifications)
})
</script>
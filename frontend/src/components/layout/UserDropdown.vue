<template>
  <Dropdown
    :items="userMenuItems"
    align="right"
    width="w-56"
    trigger-class="w-full"
  >
    <template #trigger>
      <div 
        class="flex items-center w-full p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-700 transition-colors cursor-pointer"
        :class="{ 'justify-center': collapsed }"
      >
        <img
          :src="user.avatar"
          :alt="user.name"
          class="h-8 w-8 rounded-full object-cover"
        />
        <div v-if="!collapsed" class="ml-3 flex-1 min-w-0">
          <p class="text-sm font-medium text-gray-900 dark:text-white truncate">
            {{ user.name }}
          </p>
          <p class="text-xs text-gray-500 dark:text-gray-400 truncate">
            {{ user.email }}
          </p>
        </div>
        <ChevronsUpDown
          v-if="!collapsed"
          class="h-4 w-4 text-gray-400 ml-2 flex-shrink-0"
        />
      </div>
    </template>
  </Dropdown>
</template>

<script setup>
import { ref, computed } from 'vue'
import { 
  ChevronsUpDown, 
  UserIcon, 
  CogIcon, 
  BellIcon, 
  CreditCardIcon, 
  LogOutIcon 
} from 'lucide-vue-next'
import Dropdown from '@/components/ui/Dropdown.vue'

const props = defineProps({
  collapsed: {
    type: Boolean,
    default: false
  }
})

const user = ref({
  name: 'John Doe',
  email: 'john@example.com',
  avatar: 'https://via.placeholder.com/32/6B7280/ffffff?text=JD'
})

const userMenuItems = computed(() => [
  [
    {
      label: 'Profile',
      icon: UserIcon,
      to: '/profile'
    },
    {
      label: 'Settings',
      icon: CogIcon,
      to: '/settings'
    },
    {
      label: 'Notifications',
      icon: BellIcon,
      to: '/notifications'
    }
  ],
  [
    {
      label: 'Billing',
      icon: CreditCardIcon,
      to: '/billing'
    }
  ],
  [
    {
      label: 'Sign out',
      icon: LogOutIcon,
      onSelect() {
        handleSignOut()
      }
    }
  ]
])

const handleSignOut = () => {
  // Handle sign out logic
  console.log('Signing out...')
  // You might want to clear tokens, redirect to login, etc.
}
</script>
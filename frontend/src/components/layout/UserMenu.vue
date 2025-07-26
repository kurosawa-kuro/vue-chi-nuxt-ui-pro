<template>
  <Dropdown
    :items="userMenuItems"
    align="right"
    width="w-56"
  >
    <template #trigger>
      <button class="flex items-center p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-700 transition-colors">
        <img
          :src="user.avatar"
          :alt="user.name"
          class="h-8 w-8 rounded-full object-cover"
        />
        <span class="sr-only">Open user menu</span>
      </button>
    </template>
  </Dropdown>
</template>

<script setup>
import { ref, computed } from 'vue'
import { 
  UserIcon, 
  CogIcon, 
  BellIcon, 
  CreditCardIcon, 
  LogOutIcon 
} from 'lucide-vue-next'
import Dropdown from '@/components/ui/Dropdown.vue'

const user = ref({
  name: 'John Doe',
  email: 'john@example.com',
  avatar: 'https://via.placeholder.com/32/6B7280/ffffff?text=JD'
})

const userMenuItems = computed(() => [
  [
    {
      label: user.value.name,
      description: user.value.email,
      disabled: true
    }
  ],
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
  console.log('Signing out...')
}
</script>
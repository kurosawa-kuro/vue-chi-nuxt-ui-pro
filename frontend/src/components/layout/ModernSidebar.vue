<template>
  <div class="flex h-full">
    <!-- Sidebar backdrop (mobile) -->
    <div
      v-if="isMobile && modelValue"
      class="fixed inset-0 z-40 bg-gray-900/50 lg:hidden"
      @click="$emit('update:open', false)"
    />

    <!-- Sidebar -->
    <div
      ref="sidebarRef"
      :class="sidebarClasses"
      class="relative flex flex-col bg-white dark:bg-gray-800 border-r border-gray-200 dark:border-gray-700 transition-all duration-300 ease-in-out"
    >
      <!-- Header -->
      <div class="flex items-center justify-between p-4 border-b border-gray-200 dark:border-gray-700">
        <TeamsDropdown :collapsed="collapsed" />
        
        <!-- Mobile close button -->
        <button
          v-if="isMobile"
          @click="$emit('update:open', false)"
          class="lg:hidden p-2 rounded-lg text-gray-400 hover:text-gray-600 hover:bg-gray-100"
        >
          <X class="h-5 w-5" />
        </button>
      </div>

      <!-- Search Button -->
      <div class="p-4">
        <SearchButton :collapsed="collapsed" />
      </div>

      <!-- Navigation -->
      <nav class="flex-1 px-4 pb-4 space-y-2">
        <div class="space-y-1">
          <template v-for="item in navigationItems" :key="item.label">
            <NavigationItem
              :item="item"
              :collapsed="collapsed"
              :active="isActive(item)"
            />
          </template>
        </div>

        <!-- Secondary Navigation -->
        <div class="border-t border-gray-200 dark:border-gray-700 pt-4 mt-8">
          <div class="space-y-1">
            <template v-for="item in secondaryItems" :key="item.label">
              <NavigationItem
                :item="item"
                :collapsed="collapsed"
                :active="isActive(item)"
              />
            </template>
          </div>
        </div>
      </nav>

      <!-- Footer -->
      <div class="border-t border-gray-200 dark:border-gray-700 p-4">
        <UserDropdown :collapsed="collapsed" />
      </div>

      <!-- Resize handle -->
      <div
        v-if="resizable && !isMobile"
        class="absolute right-0 top-0 h-full w-1 cursor-col-resize bg-transparent hover:bg-primary-500 transition-colors"
        @mousedown="startResize"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { useRoute } from 'vue-router'
import { X, HomeIcon, InboxIcon, UsersIcon, CogIcon, MessageCircleIcon, HelpCircleIcon } from 'lucide-vue-next'

import TeamsDropdown from './TeamsDropdown.vue'
import SearchButton from './SearchButton.vue'
import NavigationItem from './NavigationItem.vue'
import UserDropdown from './UserDropdown.vue'

const props = defineProps({
  modelValue: {
    type: Boolean,
    default: false
  },
  collapsible: {
    type: Boolean,
    default: true
  },
  resizable: {
    type: Boolean,
    default: false
  },
  defaultWidth: {
    type: Number,
    default: 256
  }
})

const emit = defineEmits(['update:open'])

const route = useRoute()
const sidebarRef = ref(null)
const currentWidth = ref(props.defaultWidth)
const collapsed = ref(false)
const isResizing = ref(false)
const isMobile = ref(false)

const navigationItems = ref([
  {
    label: 'Home',
    icon: HomeIcon,
    to: '/',
    badge: null
  },
  {
    label: 'Hello World',
    icon: MessageCircleIcon,
    to: '/hello-world',
    badge: null
  },
  {
    label: 'Inbox',
    icon: InboxIcon,
    to: '/inbox',
    badge: '4'
  },
  {
    label: 'Customers',
    icon: UsersIcon,
    to: '/customers',
    badge: null
  },
  {
    label: 'Settings',
    icon: CogIcon,
    to: '/settings',
    children: [
      { label: 'General', to: '/settings' },
      { label: 'Members', to: '/settings/members' },
      { label: 'Notifications', to: '/settings/notifications' },
      { label: 'Security', to: '/settings/security' }
    ]
  }
])

const secondaryItems = ref([
  {
    label: 'Feedback',
    icon: MessageCircleIcon,
    to: 'https://github.com/your-repo',
    target: '_blank'
  },
  {
    label: 'Help & Support',
    icon: HelpCircleIcon,
    to: 'https://docs.your-app.com',
    target: '_blank'
  }
])

const sidebarClasses = computed(() => {
  const classes = []
  
  if (isMobile.value) {
    classes.push(
      'fixed inset-y-0 left-0 z-50 w-64 transform lg:relative lg:translate-x-0',
      props.modelValue ? 'translate-x-0' : '-translate-x-full'
    )
  } else {
    classes.push(
      'relative',
      collapsed.value ? 'w-16' : `w-64`
    )
  }
  
  return classes.join(' ')
})

const isActive = (item) => {
  if (item.to && typeof item.to === 'string' && !item.to.startsWith('http')) {
    return route.path === item.to
  }
  return false
}

const checkMobile = () => {
  isMobile.value = window.innerWidth < 1024
  if (isMobile.value) {
    collapsed.value = false
  }
}

const startResize = (e) => {
  isResizing.value = true
  document.addEventListener('mousemove', handleResize)
  document.addEventListener('mouseup', stopResize)
  e.preventDefault()
}

const handleResize = (e) => {
  if (!isResizing.value) return
  
  const newWidth = e.clientX
  if (newWidth >= 200 && newWidth <= 400) {
    currentWidth.value = newWidth
    collapsed.value = newWidth < 220
  }
}

const stopResize = () => {
  isResizing.value = false
  document.removeEventListener('mousemove', handleResize)
  document.removeEventListener('mouseup', stopResize)
}

onMounted(() => {
  checkMobile()
  window.addEventListener('resize', checkMobile)
})

onUnmounted(() => {
  window.removeEventListener('resize', checkMobile)
  document.removeEventListener('mousemove', handleResize)
  document.removeEventListener('mouseup', stopResize)
})
</script>
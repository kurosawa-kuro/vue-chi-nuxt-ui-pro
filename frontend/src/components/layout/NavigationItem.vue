<template>
  <div>
    <!-- Main navigation item -->
    <component
      :is="item.to ? 'router-link' : 'button'"
      :to="item.to"
      :target="item.target"
      @click="handleClick"
      :class="itemClasses"
      class="group flex items-center w-full p-2 rounded-lg transition-colors"
    >
      <component
        :is="item.icon"
        class="h-5 w-5 flex-shrink-0"
        :class="iconClasses"
      />
      
      <span 
        v-if="!collapsed"
        class="ml-3 text-sm font-medium truncate"
        :class="textClasses"
      >
        {{ item.label }}
      </span>
      
      <span
        v-if="item.badge && !collapsed"
        class="ml-auto inline-flex items-center rounded-full px-2 py-0.5 text-xs font-medium"
        :class="badgeClasses"
      >
        {{ item.badge }}
      </span>
      
      <ChevronRightIcon
        v-if="hasChildren && !collapsed"
        class="ml-auto h-4 w-4 transition-transform duration-200"
        :class="[
          'text-gray-400',
          expanded ? 'rotate-90' : ''
        ]"
      />
    </component>

    <!-- Children (submenu) -->
    <Transition
      enter-active-class="transition duration-200 ease-out"
      enter-from-class="opacity-0 -translate-y-1"
      enter-to-class="opacity-100 translate-y-0"
      leave-active-class="transition duration-150 ease-in"
      leave-from-class="opacity-100 translate-y-0"
      leave-to-class="opacity-0 -translate-y-1"
    >
      <div v-if="expanded && hasChildren && !collapsed" class="mt-1 ml-8">
        <template v-for="child in item.children" :key="child.label">
          <router-link
            :to="child.to"
            class="group flex items-center w-full p-2 text-sm rounded-lg transition-colors"
            :class="isChildActive(child) ? 
              'text-primary-600 bg-primary-50 dark:bg-primary-900/20' : 
              'text-gray-600 dark:text-gray-300 hover:text-gray-900 dark:hover:text-white hover:bg-gray-100 dark:hover:bg-gray-700'"
          >
            {{ child.label }}
          </router-link>
        </template>
      </div>
    </Transition>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'
import { useRoute } from 'vue-router'
import { ChevronRightIcon } from 'lucide-vue-next'

const props = defineProps({
  item: {
    type: Object,
    required: true
  },
  collapsed: {
    type: Boolean,
    default: false
  },
  active: {
    type: Boolean,
    default: false
  }
})

const route = useRoute()
const expanded = ref(false)

const hasChildren = computed(() => {
  return props.item.children && props.item.children.length > 0
})

const itemClasses = computed(() => {
  if (props.active) {
    return 'text-primary-600 bg-primary-50 dark:bg-primary-900/20'
  }
  return 'text-gray-700 dark:text-gray-200 hover:text-gray-900 dark:hover:text-white hover:bg-gray-100 dark:hover:bg-gray-700'
})

const iconClasses = computed(() => {
  if (props.active) {
    return 'text-primary-600'
  }
  return 'text-gray-400 group-hover:text-gray-500'
})

const textClasses = computed(() => {
  if (props.active) {
    return 'text-primary-600'
  }
  return 'text-gray-700 dark:text-gray-200 group-hover:text-gray-900 dark:group-hover:text-white'
})

const badgeClasses = computed(() => {
  if (props.active) {
    return 'bg-primary-100 text-primary-600 dark:bg-primary-900/20'
  }
  return 'bg-gray-100 text-gray-600 dark:bg-gray-700 dark:text-gray-300'
})

const isChildActive = (child) => {
  return route.path === child.to
}

const handleClick = () => {
  if (hasChildren.value && !props.collapsed) {
    expanded.value = !expanded.value
  }
}
</script>
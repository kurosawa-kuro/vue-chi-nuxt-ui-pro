<template>
  <div class="relative" ref="dropdownRef">
    <button
      @click="toggle"
      @keydown.escape="close"
      :class="triggerClasses"
      :aria-expanded="isOpen"
      aria-haspopup="true"
    >
      <slot name="trigger">
        <span>{{ triggerText }}</span>
        <ChevronDownIcon 
          class="h-4 w-4 transition-transform duration-200"
          :class="{ 'rotate-180': isOpen }"
        />
      </slot>
    </button>

    <Transition
      enter-active-class="transition ease-out duration-100"
      enter-from-class="transform opacity-0 scale-95"
      enter-to-class="transform opacity-100 scale-100"
      leave-active-class="transition ease-in duration-75"
      leave-from-class="transform opacity-100 scale-100"
      leave-to-class="transform opacity-0 scale-95"
    >
      <div
        v-if="isOpen"
        :class="menuClasses"
        role="menu"
        aria-orientation="vertical"
      >
        <div class="py-1">
          <slot name="content" :close="close">
            <template v-for="(group, groupIndex) in items" :key="groupIndex">
              <div v-if="groupIndex > 0" class="border-t border-gray-100 my-1"></div>
              <template v-for="item in group" :key="item.label">
                <component
                  :is="item.to ? 'router-link' : 'button'"
                  :to="item.to"
                  :target="item.target"
                  @click="handleItemClick(item)"
                  :class="itemClasses"
                  role="menuitem"
                >
                  <component
                    v-if="item.icon"
                    :is="item.icon"
                    class="h-4 w-4 text-gray-400"
                  />
                  <span>{{ item.label }}</span>
                  <span
                    v-if="item.badge"
                    class="ml-auto inline-flex items-center rounded-full bg-gray-100 px-2 py-0.5 text-xs font-medium text-gray-800"
                  >
                    {{ item.badge }}
                  </span>
                </component>
              </template>
            </template>
          </slot>
        </div>
      </div>
    </Transition>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import { ChevronDownIcon } from 'lucide-vue-next'

const props = defineProps({
  items: {
    type: Array,
    default: () => []
  },
  triggerText: {
    type: String,
    default: 'Options'
  },
  align: {
    type: String,
    default: 'left',
    validator: (value) => ['left', 'right', 'center'].includes(value)
  },
  width: {
    type: String,
    default: 'w-56'
  },
  triggerClass: {
    type: String,
    default: ''
  }
})

const emit = defineEmits(['select'])

const dropdownRef = ref(null)
const isOpen = ref(false)

const triggerClasses = computed(() => {
  const base = 'inline-flex items-center justify-center gap-2 rounded-lg border border-gray-300 dark:border-gray-600 bg-white dark:bg-gray-800 px-3 py-2 text-sm font-medium text-gray-700 dark:text-gray-200 shadow-sm hover:bg-gray-50 dark:hover:bg-gray-700 focus:outline-none focus:ring-2 focus:ring-primary-500 focus:ring-offset-2'
  return props.triggerClass ? `${base} ${props.triggerClass}` : base
})

const menuClasses = computed(() => {
  const alignmentClass = {
    left: 'left-0',
    right: 'right-0',
    center: 'left-1/2 transform -translate-x-1/2'
  }[props.align]

  return `absolute z-10 mt-2 ${props.width} ${alignmentClass} rounded-lg bg-white dark:bg-gray-800 shadow-lg ring-1 ring-black dark:ring-white ring-opacity-5 dark:ring-opacity-10 focus:outline-none`
})

const itemClasses = 'group flex w-full items-center gap-3 px-4 py-2 text-sm text-gray-700 dark:text-gray-200 hover:bg-gray-100 dark:hover:bg-gray-700 hover:text-gray-900 dark:hover:text-gray-100'

const toggle = () => {
  isOpen.value = !isOpen.value
}

const close = () => {
  isOpen.value = false
}

const handleItemClick = (item) => {
  if (item.onSelect) {
    item.onSelect()
  }
  emit('select', item)
  close()
}

const handleClickOutside = (event) => {
  if (dropdownRef.value && !dropdownRef.value.contains(event.target)) {
    close()
  }
}

onMounted(() => {
  document.addEventListener('click', handleClickOutside)
})

onUnmounted(() => {
  document.removeEventListener('click', handleClickOutside)
})
</script>
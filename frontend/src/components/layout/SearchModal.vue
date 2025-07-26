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
        class="fixed inset-0 z-50 overflow-y-auto"
        @click="close"
      >
        <div class="flex min-h-screen items-start justify-center p-4 pt-16">
          <div class="fixed inset-0 bg-gray-900/50 backdrop-blur-sm" />
          
          <div
            @click.stop
            class="relative w-full max-w-2xl bg-white dark:bg-gray-800 rounded-xl shadow-2xl ring-1 ring-black/5 dark:ring-white/10"
          >
            <!-- Search input -->
            <div class="flex items-center px-4 py-4 border-b border-gray-200 dark:border-gray-700">
              <SearchIcon class="h-5 w-5 text-gray-400 mr-3" />
              <input
                ref="searchInput"
                v-model="query"
                type="text"
                placeholder="Search..."
                class="flex-1 bg-transparent text-gray-900 dark:text-white placeholder-gray-500 outline-none"
                @keydown.escape="close"
                @keydown.down="highlightNext"
                @keydown.up="highlightPrevious"
                @keydown.enter="selectHighlighted"
              />
              <div class="flex items-center space-x-1 text-xs text-gray-400">
                <kbd class="px-1.5 py-0.5 bg-gray-100 dark:bg-gray-700 rounded">ESC</kbd>
                <span>to close</span>
              </div>
            </div>

            <!-- Search results -->
            <div class="max-h-96 overflow-y-auto">
              <div v-if="loading" class="flex items-center justify-center p-8">
                <div class="h-6 w-6 animate-spin rounded-full border-2 border-primary-600 border-t-transparent" />
              </div>

              <div v-else-if="!query" class="p-6 text-center text-gray-500 dark:text-gray-400">
                <SearchIcon class="h-12 w-12 mx-auto mb-4 text-gray-300" />
                <p class="text-lg font-medium mb-2">Search everything</p>
                <p class="text-sm">Start typing to search through pages, users, and settings</p>
              </div>

              <div v-else-if="results.length === 0" class="p-6 text-center text-gray-500 dark:text-gray-400">
                <p>No results found for "{{ query }}"</p>
              </div>

              <div v-else class="p-2">
                <template v-for="(group, groupIndex) in groupedResults" :key="group.label">
                  <div v-if="groupIndex > 0" class="border-t border-gray-200 dark:border-gray-700 my-2" />
                  
                  <div class="mb-4">
                    <h3 class="px-3 py-2 text-xs font-semibold text-gray-400 uppercase tracking-wider">
                      {{ group.label }}
                    </h3>
                    
                    <div class="space-y-1">
                      <button
                        v-for="(item, itemIndex) in group.items"
                        :key="item.id"
                        @click="selectItem(item)"
                        @mouseenter="highlightedIndex = getGlobalIndex(groupIndex, itemIndex)"
                        :class="[
                          'w-full text-left px-3 py-2 rounded-lg transition-colors',
                          highlightedIndex === getGlobalIndex(groupIndex, itemIndex)
                            ? 'bg-primary-50 dark:bg-primary-900/20 text-primary-700 dark:text-primary-300'
                            : 'hover:bg-gray-100 dark:hover:bg-gray-700'
                        ]"
                      >
                        <div class="flex items-center">
                          <component
                            :is="item.icon"
                            class="h-4 w-4 text-gray-400 mr-3"
                          />
                          <div class="flex-1">
                            <div class="text-sm font-medium text-gray-900 dark:text-white">
                              {{ item.title }}
                            </div>
                            <div v-if="item.description" class="text-xs text-gray-500 dark:text-gray-400">
                              {{ item.description }}
                            </div>
                          </div>
                        </div>
                      </button>
                    </div>
                  </div>
                </template>
              </div>
            </div>
          </div>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

<script setup>
import { ref, computed, watch, nextTick, onMounted, onUnmounted } from 'vue'
import { useRouter } from 'vue-router'
import { SearchIcon, HomeIcon, UsersIcon, CogIcon, FileTextIcon } from 'lucide-vue-next'

const router = useRouter()
const isOpen = ref(false)
const query = ref('')
const loading = ref(false)
const searchInput = ref(null)
const highlightedIndex = ref(0)

const mockResults = ref([
  { id: 1, title: 'Home', description: 'Dashboard overview', to: '/', icon: HomeIcon, type: 'page' },
  { id: 2, title: 'Hello World', description: 'Sample page', to: '/hello-world', icon: FileTextIcon, type: 'page' },
  { id: 3, title: 'Users', description: 'Manage users', to: '/users', icon: UsersIcon, type: 'page' },
  { id: 4, title: 'Settings', description: 'Application settings', to: '/settings', icon: CogIcon, type: 'page' },
])

const results = computed(() => {
  if (!query.value) return []
  
  return mockResults.value.filter(item =>
    item.title.toLowerCase().includes(query.value.toLowerCase()) ||
    item.description.toLowerCase().includes(query.value.toLowerCase())
  )
})

const groupedResults = computed(() => {
  const groups = [
    {
      label: 'Pages',
      items: results.value.filter(item => item.type === 'page')
    },
    {
      label: 'Users',
      items: results.value.filter(item => item.type === 'user')
    },
    {
      label: 'Settings',
      items: results.value.filter(item => item.type === 'setting')
    }
  ].filter(group => group.items.length > 0)
  
  return groups
})

const totalResults = computed(() => {
  return groupedResults.value.reduce((total, group) => total + group.items.length, 0)
})

const getGlobalIndex = (groupIndex, itemIndex) => {
  let index = 0
  for (let i = 0; i < groupIndex; i++) {
    index += groupedResults.value[i].items.length
  }
  return index + itemIndex
}

const getItemByGlobalIndex = (globalIndex) => {
  let currentIndex = 0
  for (const group of groupedResults.value) {
    for (const item of group.items) {
      if (currentIndex === globalIndex) {
        return item
      }
      currentIndex++
    }
  }
  return null
}

const open = () => {
  isOpen.value = true
  nextTick(() => {
    searchInput.value?.focus()
  })
}

const close = () => {
  isOpen.value = false
  query.value = ''
  highlightedIndex.value = 0
}

const selectItem = (item) => {
  if (item.to) {
    router.push(item.to)
  }
  close()
}

const selectHighlighted = () => {
  const item = getItemByGlobalIndex(highlightedIndex.value)
  if (item) {
    selectItem(item)
  }
}

const highlightNext = () => {
  if (highlightedIndex.value < totalResults.value - 1) {
    highlightedIndex.value++
  }
}

const highlightPrevious = () => {
  if (highlightedIndex.value > 0) {
    highlightedIndex.value--
  }
}

const handleKeydown = (e) => {
  if ((e.metaKey || e.ctrlKey) && e.key === 'k') {
    e.preventDefault()
    open()
  }
}

const handleOpenSearch = () => {
  open()
}

watch(query, () => {
  highlightedIndex.value = 0
})

onMounted(() => {
  document.addEventListener('keydown', handleKeydown)
  window.addEventListener('open-search', handleOpenSearch)
})

onUnmounted(() => {
  document.removeEventListener('keydown', handleKeydown)
  window.removeEventListener('open-search', handleOpenSearch)
})
</script>
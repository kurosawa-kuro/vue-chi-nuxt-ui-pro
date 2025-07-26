<template>
  <Dropdown
    :items="dropdownItems"
    :width="collapsed ? 'w-40' : 'w-full'"
    align="left"
    trigger-class="w-full"
  >
    <template #trigger>
      <div 
        class="flex items-center w-full p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-700 transition-colors cursor-pointer"
        :class="{ 'justify-center': collapsed }"
      >
        <img
          :src="selectedTeam.avatar.src"
          :alt="selectedTeam.avatar.alt"
          class="h-8 w-8 rounded-lg object-cover"
        />
        <div v-if="!collapsed" class="ml-3 flex-1 min-w-0">
          <p class="text-sm font-medium text-gray-900 dark:text-white truncate">
            {{ selectedTeam.label }}
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
import { ChevronsUpDown, PlusCircle, Cog } from 'lucide-vue-next'
import Dropdown from '@/components/ui/Dropdown.vue'

const props = defineProps({
  collapsed: {
    type: Boolean,
    default: false
  }
})

const teams = ref([
  {
    label: 'Vue Chi',
    avatar: {
      src: 'https://via.placeholder.com/32/00DC82/ffffff?text=VC',
      alt: 'Vue Chi'
    }
  },
  {
    label: 'Frontend Team',
    avatar: {
      src: 'https://via.placeholder.com/32/3B82F6/ffffff?text=FT',
      alt: 'Frontend Team'
    }
  },
  {
    label: 'Backend Team',
    avatar: {
      src: 'https://via.placeholder.com/32/8B5CF6/ffffff?text=BT',
      alt: 'Backend Team'
    }
  }
])

const selectedTeam = ref(teams.value[0])

const dropdownItems = computed(() => [
  teams.value.map(team => ({
    ...team,
    onSelect() {
      selectedTeam.value = team
    }
  })),
  [
    {
      label: 'Create team',
      icon: PlusCircle,
      onSelect() {
        // Handle create team
        console.log('Create team')
      }
    },
    {
      label: 'Manage teams',
      icon: Cog,
      onSelect() {
        // Handle manage teams
        console.log('Manage teams')
      }
    }
  ]
])
</script>
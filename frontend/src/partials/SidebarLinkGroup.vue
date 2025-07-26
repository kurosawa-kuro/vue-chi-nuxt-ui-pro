<template>
  <li class="px-3 py-2 rounded-xl mb-1 last:mb-0 transition-colors" :class="activeCondition && 'bg-primary-50 dark:bg-primary-500/10 border border-primary-200 dark:border-primary-500/20'">
    <slot :handleClick="handleClick" :expanded="expanded" />
  </li>
</template>

<script>
import { ref } from 'vue'

export default {
  name: 'SidebarLinkGroup',
  props: ['activeCondition'],
  setup(props) {
    const expanded = ref(props.activeCondition)

    const handleClick = () => {
      expanded.value = !expanded.value
    }

    return {
      expanded,
      handleClick,
    }
  },
}
</script>
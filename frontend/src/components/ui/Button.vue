<template>
  <button
    :type="type"
    :class="buttonClasses"
    :disabled="disabled || loading"
    @click="$emit('click', $event)"
  >
    <component
      v-if="leadingIcon && !loading"
      :is="leadingIcon"
      class="h-4 w-4"
    />
    <div
      v-if="loading"
      class="h-4 w-4 animate-spin rounded-full border-2 border-current border-t-transparent"
    />
    <span v-if="label || $slots.default">
      <slot>{{ label }}</slot>
    </span>
    <component
      v-if="trailingIcon && !loading"
      :is="trailingIcon"
      class="h-4 w-4"
    />
  </button>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  type: {
    type: String,
    default: 'button'
  },
  variant: {
    type: String,
    default: 'primary',
    validator: (value) => ['primary', 'secondary', 'outline', 'ghost', 'link'].includes(value)
  },
  size: {
    type: String,
    default: 'md',
    validator: (value) => ['xs', 'sm', 'md', 'lg', 'xl'].includes(value)
  },
  color: {
    type: String,
    default: 'primary'
  },
  disabled: {
    type: Boolean,
    default: false
  },
  loading: {
    type: Boolean,
    default: false
  },
  block: {
    type: Boolean,
    default: false
  },
  square: {
    type: Boolean,
    default: false
  },
  label: {
    type: String,
    default: ''
  },
  leadingIcon: {
    type: [String, Object],
    default: null
  },
  trailingIcon: {
    type: [String, Object],
    default: null
  }
})

const emit = defineEmits(['click'])

const baseClasses = 'inline-flex items-center justify-center font-medium transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-offset-2 disabled:pointer-events-none disabled:opacity-50'

const variantClasses = {
  primary: 'bg-primary-600 text-white hover:bg-primary-700 focus-visible:ring-primary-600',
  secondary: 'bg-gray-100 text-gray-900 hover:bg-gray-200 focus-visible:ring-gray-500',
  outline: 'border border-gray-300 bg-transparent text-gray-700 hover:bg-gray-50 focus-visible:ring-gray-500',
  ghost: 'bg-transparent text-gray-700 hover:bg-gray-100 focus-visible:ring-gray-500',
  link: 'bg-transparent text-primary-600 underline-offset-4 hover:underline focus-visible:ring-primary-600'
}

const sizeClasses = {
  xs: 'h-6 px-2 text-xs gap-1',
  sm: 'h-8 px-3 text-sm gap-1.5',
  md: 'h-10 px-4 text-sm gap-2',
  lg: 'h-12 px-6 text-base gap-2',
  xl: 'h-14 px-8 text-lg gap-2.5'
}

const buttonClasses = computed(() => {
  const classes = [baseClasses]
  
  classes.push(variantClasses[props.variant])
  classes.push(sizeClasses[props.size])
  
  if (props.block) {
    classes.push('w-full')
  }
  
  if (props.square) {
    const squareSize = sizeClasses[props.size].match(/h-(\d+)/)?.[1]
    if (squareSize) {
      classes.push(`w-${squareSize}`)
    }
  }
  
  if (props.variant !== 'link') {
    classes.push('rounded-lg')
  }
  
  return classes.join(' ')
})
</script>
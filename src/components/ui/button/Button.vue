<script setup lang="ts">
import { computed } from 'vue'
import { cn } from '@/lib/utils'

const props = withDefaults(
  defineProps<{
    variant?: 'default' | 'secondary' | 'outline' | 'ghost' | 'destructive'
    size?: 'sm' | 'default' | 'lg' | 'icon'
    class?: string
  }>(),
  {
    variant: 'default',
    size: 'default',
  },
)

const classes = computed(() =>
  cn(
    'inline-flex items-center justify-center gap-2 whitespace-nowrap rounded-md text-sm font-semibold transition-colors focus-visible:outline-none focus-visible:ring-2 focus-visible:ring-ring disabled:pointer-events-none disabled:opacity-50',
    {
      'bg-primary text-primary-foreground hover:bg-blue-700': props.variant === 'default',
      'bg-secondary text-secondary-foreground hover:bg-teal-800': props.variant === 'secondary',
      'border border-input bg-card hover:bg-muted': props.variant === 'outline',
      'hover:bg-muted': props.variant === 'ghost',
      'bg-destructive text-destructive-foreground hover:bg-red-700': props.variant === 'destructive',
      'h-8 px-3 text-xs': props.size === 'sm',
      'h-10 px-4 py-2': props.size === 'default',
      'h-11 px-6': props.size === 'lg',
      'h-10 w-10': props.size === 'icon',
    },
    props.class,
  ),
)
</script>

<template>
  <button :class="classes">
    <slot />
  </button>
</template>

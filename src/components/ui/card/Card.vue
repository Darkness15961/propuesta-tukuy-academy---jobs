<script setup lang="ts">
import { cn } from '@/lib/utils'

defineProps<{ class?: string }>()
</script>

<template>
  <div
    :class="
      cn(
        'rounded-lg border border-border bg-card text-card-foreground shadow-sm transition-all duration-300 ease-out hover:-translate-y-0.5 hover:shadow-lg',
        $props.class,
      )
    "
  >
    <slot />
  </div>
</template>

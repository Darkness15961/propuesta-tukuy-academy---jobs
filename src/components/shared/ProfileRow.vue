<script setup lang="ts">
defineProps<{
  label: string
  value: string
}>()
</script>

<template>
  <div class="flex justify-between gap-4 rounded-lg border border-border p-3">
    <span class="text-muted-foreground">{{ label }}</span>
    <strong class="text-right">{{ value }}</strong>
  </div>
</template>

<script setup lang="ts">
defineProps<{
  eyebrow: string
  title: string
  description: string
}>()
</script>

<template>
  <div class="grid gap-1">
    <p class="text-xs font-bold uppercase text-secondary">{{ eyebrow }}</p>
    <h1 class="text-3xl font-bold tracking-normal">{{ title }}</h1>
    <p class="max-w-2xl text-muted-foreground">{{ description }}</p>
  </div>
</template>

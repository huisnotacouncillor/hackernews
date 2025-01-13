<script setup lang="ts">
defineProps<{
  loading: boolean
}>()
</script>

<template>
  <div
    v-if="loading"
    style="text-align:center; padding: 1rem;"
  >
    <LoadSpinner />
  </div>
  <slot v-else />
</template>

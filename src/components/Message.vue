<script setup lang="ts">
defineProps<{
  message: string;
  byOwner: boolean;
}>();
</script>

<template>
  <div class="message-container py-2 px-4" :class="byOwner ? 'byOwner' : ''">
    <div class="message pa-4 rounded-xl">{{ message }}</div>
  </div>
</template>

<style scoped lang="scss">
.message-container {
  display: flex;
  justify-content: left;

  &.byOwner {
    justify-content: right;
    .message {
      background-color: rgb(var(--v-theme-primary)) !important;
      color: rgb(var(--v-theme-on-primary)) !important;
    }
  }

  .message {
    background-color: white;
  }
}
</style>

<script setup lang="ts">
import { ref } from "vue";

const open = ref<boolean>(false);

function toggle(): void {
  open.value = !open.value;
}

defineProps<{
  item: {
    id: number;
    title: string;
    snippet: string;
    description: string;
  };
}>();
</script>

<template>
  <li
    class="py-3 px-4 cursor-pointer hover:bg-gray-100"
    @click="toggle"
  >
    <div class="font-medium">{{ item.title }}</div>
    <div class="text-sm text-gray-600">{{ item.snippet }}</div>

    <transition name="fade">
      <div
        v-if="open"
        class="mt-2 text-sm text-gray-700"
      >
        {{ item.description }}
      </div>
    </transition>
  </li>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.2s ease;
}
.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

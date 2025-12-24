<template>
  <div class="search-bar">
    <input type="text" placeholder="Search..." @input="onInput"
    class="w-full rounded-lg border border-gray-300 px-4 py-3 text-base focus:outline-none focus:ring-2 focus:ring-blue-500 transition" />
  </div>
</template>

<script setup lang="ts">

const props = defineProps<{
  query: string;
}>();

const emit = defineEmits<{
  (e: 'update-query', value: string): void;
}>();

function onInput(event: Event) {
  const target = event.target as HTMLInputElement;
  emit('update-query', target.value);
}
</script> 


<script setup lang="ts">
import SearchResultItem from "./SearchResultItem.vue";

type SearchResult = {
  id: number;
  title: string;
  snippet: string;
  description: string;
};

defineProps<{
  results: SearchResult[];
}>();
</script>

<template>
  <ul class="divide-y divide-gray-200">
    <SearchResultItem
      v-for="item in results"
      :key="item.id"
      :item="item"
    />
  </ul>
</template>

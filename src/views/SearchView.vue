<script setup lang="ts">
import { ref, computed } from "vue";
import SearchBar from "../components/SearchBar.vue";
import SearchResultList from "../components/SearchResultList.vue";

type SearchResult = {
  id: number;
  title: string;
  snippet: string;
  description: string;
};

const query = ref<string>("");

function handleUpdateQuery(value: string): void {
  query.value = value;
}

const results = ref<SearchResult[]>([
  {
    id: 1,
    title: "Apple",
    snippet: "A popular fruit",
    description: "Apples are rich in fiber and vitamin C."
  },
  {
    id: 2,
    title: "Banana",
    snippet: "High in potassium",
    description: "Bananas are great for quick energy."
  },
  {
    id: 3,
    title: "Orange",
    snippet: "Citrus fruit",
    description: "Oranges are well known for vitamin C."
  }
]);

const filteredResults = computed(() =>
  results.value.filter(r =>
    r.title.toLowerCase().includes(query.value.toLowerCase())
  )
);
</script>

<template>
  <div class="min-h-screen bg-gray-50 flex justify-center">
    <div class="w-full max-w-xl mt-10 px-4 space-y-4">
      <SearchBar
        :query="query"
        @update-query="handleUpdateQuery"
      />

      <SearchResultList
        :results="filteredResults"
      />
    </div>
  </div>
</template>

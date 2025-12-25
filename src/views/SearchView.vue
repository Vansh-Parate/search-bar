<script setup lang="ts">
import { ref, watch } from "vue";
import SearchBar from "../components/SearchBar.vue";
import SearchResultList from "../components/SearchResultList.vue";
import Loader from "../components/Loader.vue";

type SearchResult = {
  id: number;
  title: string;
  snippet: string;
  description: string;
};

const query = ref<string>("");
const results = ref<SearchResult[]>([]);
const loading = ref<boolean>(false);
let debounce: number | undefined;    

function handleUpdateQuery(value: string): void {
  query.value = value;
}

function fetchResults(query: string): Promise<SearchResult[]> {
  // Simulated fetch function
  return new Promise((resolve) => {
    setTimeout(() => {
      const data: SearchResult[] = [
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
      ];
      resolve(
        data.filter(item =>
          item.title.toLowerCase().includes(query.toLowerCase())
        )
    );  
    }, 500);
  });
}

watch(query,async(newQuery) => {
    if(debounce) {
        clearTimeout(debounce);
    }

    if (!newQuery) {
    results.value = [];
    return;
    }

    loading.value = true;

    debounce = window.setTimeout(async() => {
       results.value = await fetchResults(newQuery);
       loading.value = false;
    },300);
    
});

</script>

<template>
  <div class="min-h-screen bg-gray-50 flex justify-center">
    <div class="w-full max-w-xl mt-10 px-4 space-y-4">
      <SearchBar
        :query="query"
        @update-query="handleUpdateQuery"
      />

      <Loader v-if="loading" />

      <SearchResultList
        v-else
        :results="results"
      />
    </div>
  </div>
</template>

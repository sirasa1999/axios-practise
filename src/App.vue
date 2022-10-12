<template>
  <div class="grid grid-cols-3 gap-x-8 gap-y-16 pl-40 pt-20 ">
    <div class='bg-gray-200 shadow-2xl p-5 w-52 h-64 rounded-xl flex flex-col items-center group' v-for="result in results" :key="result.id">
      <a :href="result.url">
        <img :src="result.thumbnailUrl" class="rounded-sm duration-300 group-hover:scale-110" />
        <p class="p-2 hidden group-hover:block text-center">{{result.id}}</p>
      </a>
      <div class="p-2">
        <button class="bg-blue-500 text-white border border-black-900 rounded-xl flex flex-row p-1 hover:bg-blue-700">
          <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
        <path stroke-linecap="round" stroke-linejoin="round" d="M9 12.75l3 3m0 0l3-3m-3 3v-7.5M21 12a9 9 0 11-18 0 9 9 0 0118 0z" />
        </svg>
        Download
      </button>
      </div>
    </div>
  </div>
  <div class="py-10 grid justify-items-center">
    <button class="p-2 bg-purple-600 text-gray-300 border border-black-900 rounded-md hover:bg-purple-800 flex flex-row " @click="loadMore">Load More... <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
  <path stroke-linecap="round" stroke-linejoin="round" d="M19.5 5.25l-7.5 7.5-7.5-7.5m15 6l-7.5 7.5-7.5-7.5" />
</svg>
</button>
  </div>
</template>

<script setup>
import { ref, reactive } from "vue";
import axios from "axios";

let results = reactive([]);
let page = ref(1);
fetchImages()
  function fetchImages(){
    axios
  .get(`https://jsonplaceholder.typicode.com/photos?_page=${page.value}&_limit=99`)
  .then((response) => {
    // /* eslint-disable */ 
    // debugger; 
    results.value=Array.prototype.push.apply(results,response.data);
    // results.value.push(response.data)
  });
}
function loadMore(){
  page.value = page.value + 1
  fetchImages()
}
</script>

<style></style>

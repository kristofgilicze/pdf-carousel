<script setup lang="ts">
import { computed, ref, watch } from 'vue';
import PdfViewer from './components/PdfViewer.vue';

const MAX = 48;
const currentPage = ref<number>(1)

const url = computed(() => `./assets/pages/LLBG_latvany_20220223_vegleges-${currentPage.value}.pdf`);

function navLeft() {
  currentPage.value--;
}

function navRight() {
  if (currentPage.value < MAX) {
    currentPage.value++;
  }
}

// update the url when the page changes
watch(() => currentPage.value, () => {
  window.history.pushState({}, '', `?page=${currentPage.value}`);
});
</script>

<template>
  <main class="flex flex-row min-h-screen w-full gap-2 justify-around">
    <button v-show="currentPage != 1" @click="navLeft" type="button">
      <svg
        class="h-6 w-6 dark:text-white"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M7 16l-4-4m0 0l4-4m-4 4h18"
        />
      </svg>
    </button>
    <div class="flex flex-col w-full min-h-screen p-10 justify-center items-center">
      <PdfViewer :path="url" class="h-15/16" />
      <input
        v-model="currentPage"
        type="number"
        :max="MAX"
        class="h-1/16 w-32 bg-gray-300 border border-gray-300 text-gray-900 text-lg text-center rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
        required
      />
    </div>
    <button @click="navRight" type="button">
      <svg
        class="h-6 w-6 dark:text-white"
        fill="none"
        stroke="currentColor"
        viewBox="0 0 24 24"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="2"
          d="M17 8l4 4m0 0l-4 4m4-4H3"
        />
      </svg>
    </button>
  </main>
</template>

<style scoped>
main {
  background-color: #525659;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

button {
  @apply rounded-lg
   font-medium
    bg-dark-700
     m-5
      text-white
       text-sm
        text-center
         p-2.5
          inline-flex
           items-center
            dark:bg-blue-600
             hover:bg-gray-400
              focus:ring-4
               focus:ring-blue-300
                dark:hover:bg-blue-700
                dark:focus:ring-blue-800;
}
</style>

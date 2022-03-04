<script setup lang="ts">
import { ref } from 'vue';
import TopNav from './components/TopNav.vue';
import PdfViewer from './components/PdfViewer.vue';
const currentPage = ref<number>(0)

function navLeft() {
  currentPage.value--;
}

function navRight() {
  currentPage.value++;
}
</script>

<template>
  <main class="flex flex-col justify-around min-h-screen w-full gap-2">
    <TopNav class="flex-shrink" @left-nav="navLeft" @right-nav="navRight"></TopNav>
    <PdfViewer path="http://infolab.stanford.edu/pub/papers/google.pdf" class="flex-grow" />
    <footer class="flex-shrink">{{ currentPage }}</footer>
  </main>
</template>

<style scoped>
main {
  background-color: #525659;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>

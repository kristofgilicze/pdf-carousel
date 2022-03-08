<script setup lang="ts">
import { PropType } from 'vue';

const props = defineProps({
    url: {
        type: String as PropType<string>,
        default: undefined
    }
})
</script>

<template>
    <a
        class="rounded-lg font-medium bg-dark-700 m-5 text-white text-sm text-center p-2.5 inline-flex items-center dark:bg-blue-600 hover:bg-gray-400 focus:ring-4 focus:ring-blue-300 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
        :href="url"
        target="_blank"
        title="Megnyitás PDF olvasóban"
    >
        <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-6 w-6"
            fill="none"
            viewBox="0 0 24 24"
            stroke="currentColor"
            stroke-width="2"
        >
            <path
                stroke-linecap="round"
                stroke-linejoin="round"
                d="M10 6H6a2 2 0 00-2 2v10a2 2 0 002 2h10a2 2 0 002-2v-4M14 4h6m0 0v6m0-6L10 14"
            />
        </svg>
        Megnyitás PDF olvasóban
    </a>
</template>

<script setup lang="ts">
import { computed, onMounted, ref, watch } from 'vue';
import Loading from './Loading.vue';

const props = defineProps({
    path: {
        type: String,
        default: '',
    },
})

const pdfObject = ref<HTMLObjectElement>()
const loading = ref<boolean>(true)
const notLoading = computed(() => !loading.value)

watch(() => props.path, () => loading.value = true)

onMounted(() => {
    pdfObject.value?.addEventListener('load', () => {
        loading.value = false
    })
})

const opts = "#toolbar=0&navpanes=0&scrollbar=0&statusbar=0&messages=0&scrollbar=0"
const dataURL = computed(() => `${props.path}${opts}`);

</script>

<template>
    <!-- The loading indicator -->
    <div class="w-65/100 h-full flex justify-center items-center" v-show="loading" id="loading">
        <Loading class="w-12 h-12" />
    </div>

    <!-- The iframe -->
    <object
        class="w-65/100 h-full"
        v-show="notLoading"
        ref="pdfObject"
        :data="dataURL"
        type="application/pdf"
    ></object>
</template>
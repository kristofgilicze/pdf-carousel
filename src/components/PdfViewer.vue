<script setup lang="ts">
import { computed, onMounted, PropType, reactive, ref, toRefs, watch, watchEffect } from 'vue';
import Loading from './Loading.vue';

const props = defineProps({
    path: {
        type: String as PropType<string>,
        default: '',
    },
    zoom: {
        type: Number as PropType<number>,
        default: 70
    }
})

const pdfObject = ref<HTMLObjectElement>()
const loading = ref<boolean>(true)

function stopLoading() {
    loading.value = false
}

const { zoom } = toRefs(props)
const opts = computed(() => `#toolbar=0&navpanes=0&scrollbar=0&statusbar=0&messages=0&zoom=${zoom.value}`)
const dataURL = computed(() => `${props.path}${opts.value}`);
watch(dataURL, () => {
    loading.value = true
})
</script>

<template>
    <!-- The loading indicator -->
    <div class="w-80/100 h-full flex justify-center items-center" v-show="loading" id="loading">
        <Loading class="w-12 h-12" />
    </div>

    <!-- The iframe -->
    <object
        @load="stopLoading"
        class="w-80/100 h-full"
        ref="pdfObject"
        :data="dataURL"
        type="application/pdf"
    ></object>
</template>
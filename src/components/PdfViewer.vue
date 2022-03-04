<script lang="ts">
import { ref, defineComponent, h, computed } from 'vue';

export default defineComponent({
    props: {
        path: {
            type: String,
            default: '',
        },
    },
    setup(props) {
        const opts = "#toolbar=0&navpanes=0&scrollbar=0&statusbar=0&messages=0&scrollbar=0"
        const dataURL = computed(() => `${props.path}${opts}`);

        return () => h('object', {
            data: dataURL.value,
            type: "application/pdf",
            height: '100%',
            width: '100%',
        })
    },
})
</script>
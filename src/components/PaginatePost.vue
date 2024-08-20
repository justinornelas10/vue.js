<script setup>
import { computed } from 'vue';


defineProps(['start','end','maxLength'])
const emit = defineEmits(['next', 'prev'])

// const checkPrev = computed(() => {
//     if (start.value === 0) {
//         return 'true'
//     }else{
//         return 'false'
//     }
// })

</script>

<template>
    <div class="btn-group" role="group" aria-label="Basic Example">
        <button 
        @click="emit('prev')" :disabled="start <= 0"
        type="button" class="btn btn-outline-primary">
            Previous

        </button>
        <button 
        @click="emit('next')" :disabled="end >= maxLength"
        type="button" class="btn btn-primary">
            Next

        </button>
    </div>
</template>
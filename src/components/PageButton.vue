<script setup>
//PROPS
const props = defineProps(['start', 'end', 'maxLength'])

//EMITS
const emit = defineEmits(['emit-next', 'emit-prev']);

</script>

<template>
    <div class="btn-group mb-2" role="group" aria-label="Basic example">
        <button
        type="button"
        class="btn btn-outline-primary"
        @click="emit('emit-prev')"
        :disabled="start === 0"
        >Previous</button>
        
        <button
        type="button"
        class="btn btn-outline-primary"
        @click="emit('emit-next')"
        :disabled="end === maxLength"
        >Next</button>
    </div>
</template>

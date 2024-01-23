<script setup>

    //EMITS
    const emit = defineEmits(['emits-values']);

    //PROPS
    // const props = defineProps(['title', 'id', 'body'])
    const props = defineProps({
        title: String,
        id: Number,
        body: {
            type: String,
            default: 'Sin descripción'
        }
    });


</script>

<template>
    <div class="card mb-2">
        <div class="card-body">
            <h5 class="card-title">{{ props.id }} - {{ props.title }}</h5>
            <p>{{ props.body }}</p>
            <button
            class="btn btn-outline-primary"
            @click="emit('emits-values', title)"
            >
            Favorito
            </button>

        </div>
    </div>
</template>
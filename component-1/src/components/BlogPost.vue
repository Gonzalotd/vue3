<script setup>

    // defineProps(['title', 'id', 'body', 'colorText'])

    defineProps({
        title: String,
        id: Number,
        body: {
            type: String,
            default: 'Sin descripcion'
        },
        colorText: String
    });

    const emit = defineEmits(['cambiarFavoritoNombre']);

</script>

<template>
    <div class="card">
        <div class="card-body" :id="id">
            <h5 class="card-title">{{ title }}</h5>
            <p :class="`text-${colorText}`">{{ body }}</p>
            <button @click="emit('cambiarFavoritoNombre', title)" 
                class="btn btn-outline-primary">
                Favorito
            </button>
        </div>
    </div>
</template>

<style>
</style>
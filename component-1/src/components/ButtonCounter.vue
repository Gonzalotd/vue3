<script setup>
    import { ref } from 'vue'; 

    const counter = ref(0);

    const increment = () => {
        counter.value++;
    }

</script>

<template>

    <div class="container mb-5">
        <button @click="increment">
            {{ counter }}
        </button>

    </div>
</template>
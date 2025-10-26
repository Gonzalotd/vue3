<script setup>

    // import axios from 'axios';
    import { ref } from 'vue';
    import { RouterLink } from 'vue-router';
    import { useGetData } from '@/composables/getData';

    // const pokemons = ref([]);
    const { data, loading, getData, errorData } = useGetData()

    // const getData = async () => {
    //     try {
    //         const { data } = await axios.get('http://pokeapi.co/api/v2/pokemon')
    //         pokemons.value = data.results;

    //     } catch (error) {
    //         console.log(error)
    //     }
    // }

    getData('http://pokeapi.co/api/v2/pokemon');
</script>

<template>
    <h1>Pokemons</h1>
    <p v-if="loading">Cargando informacion</p>
    <div class="alert alert-danger mt-2" v-if="errorData">{{ errorData }}</div>
    <div v-if="data">
        <ul class="list-group">
            <!-- <li v-for="poke in pokemons"> -->
            <li class="list-group-item" v-for="poke in data.results">
                <router-link :to="`/pokemons/${poke.name}`">
                    {{ poke.name }}
                </router-link>
            </li>
        </ul>
        <div class="mt-2">
            <button :disabled="!data.previous" 
                class="btn btn-warning me-3" @click="getData(data.previous)">Previus</button>
            <button :disabled="!data.next"
                class="btn btn-warning" @click="getData(data.next)">Next</button>
        </div>
    </div>
</template>
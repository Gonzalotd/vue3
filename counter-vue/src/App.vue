
<script setup>
    import { ref, computed } from 'vue';

    const counter = ref(0);
    const favoriteNumber = ref([]);


    const increment = () => {
        counter.value++;
    }

    const decrement = () => {
        counter.value--;
    }

    const classCounter = computed(() => {
        if (counter.value === 0 ) return 'neutro';
        if (counter.value > 0 ) return 'positivo';
        if (counter.value < 0 ) return 'negativo';
    })

    const reset = () => {
        counter.value = 0;
        favoriteNumber.value = [];
    }

    const add = () => {
        favoriteNumber.value.push(counter.value);
    }

    const desabilitarBtn = computed(() => {
        const findNumber = favoriteNumber.value.find( num => num === counter.value);        

        return findNumber || findNumber === 0;
    })

    const verificarDesabilitado = computed(() => {

        const findNumber = favoriteNumber.value.find( num => num === counter.value);    
        
        if ( findNumber === 0  ) return 'counter-component__btn desabilitado';
        
        return findNumber ?  'counter-component__btn desabilitado' : 'counter-component__btn counter-component__btn-add';
       
    })

</script>
<!-- //counter-component__btn counter-component__btn-add -->
<template>
    <div class="counter-component">
        <div class="counter-component__display">
            <span :class="classCounter">{{ counter }}</span>
        </div>
        <div class="counter-component__btn">
            <button class="counter-component__btn counter-component__btn-increment" @click="increment">+</button>
            <button class="counter-component__btn counter-component__btn-reset" @click="reset">Reset</button>
            <button :class="verificarDesabilitado" @click="add" :disabled="desabilitarBtn">Add</button>
            <button class="counter-component__btn counter-component__btn-decrement" @click="decrement">-</button>
        </div>
        <div>
            <h2>Tus números favoritos son: </h2>
            <ul>
                <li v-for="num in favoriteNumber" :key="num" class="counter-component__list">{{ num }}</li>
            </ul>
        </div>
    </div>
 
</template>

<style scoped>
    .counter-component {
        display: flex;
        flex-direction: column;
        flex-wrap: wrap;
        align-content: center;
        justify-content: center;
        align-items: center;

    }
    .counter-component__display {
        background-color: darksalmon;
        border-radius: 0.8rem;
        font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
        font-size: 2rem;
        padding: 0.4rem 0.7rem;
        text-align: center;
        width: 33%;
    }
    .positivo {
        color: white;
    }

    .negativo {
        color: red;
    }
    .neutro {
        color: green;
    }

    .desabilitado {
        background-color: rgba(75, 69, 69, 0.663);
        color: white;
    }

    .counter-component__display-negativo {
        color: red;
    }

    .counter-component__btn {
        border: none;
        border-radius: 0.8rem;
        padding: 0.4rem 1rem;
        display: flex;
        flex-direction: row;
        flex-wrap: wrap;
        align-content: center;
        justify-content: center;
        align-items: center;
        gap: 0.6rem;
        font-family:'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
        font-size: 1.2rem;
    }

    .counter-component__btn-increment {
        background-color: brown;
        color: white;
    }
    .counter-component__btn-decrement {
        background-color: burlywood;
        color: white;
    }
    .counter-component__btn-reset {
        background-color:cadetblue;
        color: white;
    }
    .counter-component__btn-add {
        background-color: green;
        color: white;
    }

    .counter-component__list {
        list-style: none;
        padding: 0.4rem 0.9rem;
        border: 0.1rem solid gray;
        border-radius: 0.8rem;
        text-align: center;
        margin-bottom: 0.8rem;
    }

</style>

<script setup>
    import { ref, onMounted } from 'vue';

    import ButtonCounter from './components/ButtonCounter.vue';
    import BlogPost from './components/BlogPost.vue';
    import PaginatePost from './components/PaginatePost.vue';
    import LoadingSpinner from './components/LoadingSpinner.vue'

    

    // const posts = ref([
    //     {title: 'Post 1', id: 1, body: 'Descripción 1', colorText: 'primary'},
    //     {title: 'Post 2', id: 2, body: 'Descripción 2', colorText: 'secundary'},
    //     {title: 'Post 3', id: 3, colorText: 'danger'}
    // ])

    const favorito = ref("")
    const posts = ref([]);

    const postXpage = 10;
    const inicio = ref(0);
    const fin = ref(postXpage);
    const loading = ref(false);

    const next = () => {
        inicio.value += postXpage
        fin.value += postXpage;
    }

    const prev = () => {
        inicio.value = inicio.value - postXpage
        fin.value = fin.value - postXpage
    }

    const cambiarFavorito = (titlePost) => {
        favorito.value = titlePost;            
    }

    // const maxLength = computed(() => post.value.length);

    onMounted( async () => {
        loading.value = true;
        try {
            const resp = await fetch('https://jsonplaceholder.typicode.com/posts')
            posts.value = await resp.json();

        } catch (error) {
            console.log(error)
        } finally {
            loading.value = false;
        }
         
    });

    // fetch('https://jsonplaceholder.typicode.com/posts')
    //     .then(res => res.json())
    //     .then(data => posts.value = data)
    //     .catch((e) => console.log(e))
    //     .finally(() => loading.value = false)

</script>

<template>
    
    <LoadingSpinner v-if="loading"/>
    <div class="container" v-else>
        <h1>App</h1>
    
        <!-- <ButtonCounter/> -->
    
        <h2>Mi Post Favorito: {{ favorito }}</h2>
    
        <PaginatePost
            @next="next"
            @prev="prev"
            class="mb-2"
            :inicio="inicio"
            :fin="fin"
            :maxLength="posts.length"/>
    
        <BlogPost
            v-for="post in posts.slice(inicio, fin)"
            :key="post.id"
            :title="post.title"
            :id="post.id"
            :body="post.body"
            :colorText="post.colorText"
            @cambiarFavoritoNombre="cambiarFavorito"
            class="mb-2"
        ></BlogPost>
    </div>
</template>

<style>

</style>
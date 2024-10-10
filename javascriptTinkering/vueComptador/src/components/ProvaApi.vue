<template>
    <h1>Prova Api</h1>
    <div>
        <div v-for = "post in posts" :key="post.id">
            <h3>Id: {{ post.id }} - {{ post.title }}</h3>
            <p> {{ post.body }}</p>
        </div>
        <div>
            <div v-for="foto in fotos" :key="foto.id">
                <h3>Id: {{ foto.id }} - {{ foto.title}}</h3>
                <img v-bind:src ="foto.url">
            </div>
        </div>
    </div>
</template>
<script setup>
import { onMounted, ref } from 'vue';
import axios from 'axios';

const posts = ref ([])

// onMounted(
//     async () => {
//     try{
//         const resultat = await axios.get('https://jsonplaceholder.typicode.com/posts')
//         console.log(resultat.data)
//         posts.value = resultat.data

//     }catch {
//         console.log('Error')

//     }
//     })

onMounted(() => {
    fetch ('https://jsonplaceholder.typicode.com/posts')
    .then(response => response.json())
    .then (data => {
        posts.value = data
        console.log(posts.value)
    })
    .catch(error => console.log ('Error: ', error))
})

const fotos  = ref([])
onMounted(
    async () => {
    try{
        const resultat = await axios.get('https://jsonplaceholder.typicode.com/photos')
        console.log(resultat.data)
        fotos.value = resultat.data

    }catch {
        console.log('Error')

    }
    })
</script>
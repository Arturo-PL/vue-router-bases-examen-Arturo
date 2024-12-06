<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router'
import Loading from './components/Loading.vue' 

const api_key = 'b9aebfffc4d03a3ed592c36ece096062'
const base_url = `https://api.themoviedb.org/3/movie/popular?language=es-MX&page=1&api_key=${api_key}`

const isLoading = ref(true)
const nowplaying = ref([])
const getNowPlayingMovies = async () => {
    isLoading.value = true
    const resp = await fetch(base_url);
    const data = await resp.json()
    nowplaying.value = data.results.map((movie) => {
        return {
            id: movie.id,
            title: movie.title,
            overview: movie.overview,
            poster_path: movie.poster_path,
            release_date: movie.release_date
        }
    })
    isLoading.value = false
}

getNowPlayingMovies()
</script>

<template>
    <Loading v-if="isLoading"/>
    <div v-else>
        <h3 style="color: #FFD700;">Lista de las Películas Más Populares</h3>
        <template v-for="m in nowplaying" :key="m.id">
            <RouterLink :to="`/movie/${m.id}`"> {{ m.title }} </RouterLink> <br>
        </template>
    </div>
</template>

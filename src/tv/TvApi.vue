<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router'
import Loading from './components/Loading.vue'

const api_key = 'b9aebfffc4d03a3ed592c36ece096062'
const base_url = `https://api.themoviedb.org/3/trending/tv/day?language=es-MX&api_key=${api_key}`


const isLoading = ref(true)
const popularTvShows = ref([])

const getPopularTvShows = async () => {
    isLoading.value = true
    const resp = await fetch(base_url)
    const data = await resp.json()
    popularTvShows.value = data.results.map((tvShow) => {
        return {
            id: tvShow.id,
            name: tvShow.name,
            overview: tvShow.overview,
            poster_path: tvShow.poster_path,
            release_date: tvShow.first_air_date,
            origin_country: tvShow.origin_country,
            vote_average: tvShow.vote_average
        }
    })
    isLoading.value = false
}

getPopularTvShows()
</script>

<template>
    <Loading v-if="isLoading"/>
    <div v-else>
        <h3 style="color: #1E90FF;">Lista de Shows de TV</h3>
        <template v-for="tv in popularTvShows" :key="tv.id">
            <RouterLink :to="`/tv/${tv.id}`"> {{ tv.name }} </RouterLink> <br>
        </template>
    </div>
</template>

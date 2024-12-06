<script setup>
import { RouterLink, useRoute } from 'vue-router';
import axios from 'axios';
import { ref } from 'vue';

const route = useRoute()
const { id } = route.params
const movie = ref ({})

const api_key = 'b9aebfffc4d03a3ed592c36ece096062'
const url = `https://api.themoviedb.org/3/movie/${id}?language=es-MX&page=1&api_key=${api_key}`

const getDetailsMoviesById = async()=>{
    const resp = await axios.get(url);
    movie.value = resp.data
    console.log(movie.value);
}

console.log(id);
getDetailsMoviesById()

</script>

<template>
    <div class="d-flex justify-content-center align-items-center vh-100">
        <div class="card mb-3" style="max-width: 540px;">
            <div class="row g-0">
                <div class="col-md-4">
                    <img :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" class="card-img img-fluid" alt="Poster"/>
                </div>
                <div class="col-md-8">
                    <div class="card-body">
                        <h5 class="card-title">{{ movie.title }}</h5>
                        <p class="card-text">{{ movie.overview }}</p>
                        <p class="card-text"><strong>Fecha de estreno:</strong> {{ movie.release_date }}</p>
                        <p class="card-text"><strong>Id de la película:</strong> {{ movie.id }}</p>
                        <RouterLink class="btn btn-success" to="/movie">Regresar</RouterLink>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>




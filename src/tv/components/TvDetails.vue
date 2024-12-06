<script setup>
import { RouterLink, useRoute } from 'vue-router'
import axios from 'axios';
import { ref } from 'vue';

const route = useRoute()
const { id } = route.params
const tvShow = ref({})

const api_key = 'b9aebfffc4d03a3ed592c36ece096062'
const url = `https://api.themoviedb.org/3/tv/${id}?language=es-MX&api_key=${api_key}`

const getTvShowDetails = async () => {
    const resp = await axios.get(url);
    tvShow.value = resp.data
    console.log(tvShow.value);
}

console.log(id)
getTvShowDetails()

</script>

<template>
    <div class="d-flex justify-content-center align-items-center vh-100">
        <div class="card mb-3" style="max-width: 540px;">
            <div class="row g-0">
                <div class="col-md-4">
                    <img :src="'https://image.tmdb.org/t/p/w500/' + tvShow.poster_path" class="card-img img-fluid" alt="Poster"/>
                </div>
                <div class="col-md-8">
                    <div class="card-body">
                        <h5 class="card-title">{{ tvShow.name }}</h5>
                        <p class="card-text">{{ tvShow.overview }}</p>
                        <p class="card-text"><strong>Primera emisión: </strong>{{ tvShow.first_air_date }}</p>
                        <p class="card-text"><strong>Id de la serie: </strong>{{ tvShow.id }}</p>
                        <p class="card-text"><strong>País de Origen: </strong>{{ tvShow.origin_country }}</p>
                        <p class="card-text"><strong>Calificación: </strong>{{ tvShow.vote_average }}</p>
                        <RouterLink class="btn btn-success" to="/tv">Regresar</RouterLink>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>


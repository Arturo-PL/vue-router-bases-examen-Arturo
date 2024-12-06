<script setup>
import { RouterLink, useRoute } from 'vue-router'
import { ref } from 'vue'

const route = useRoute()
const { id } = route.params
const post = ref({})

const base_url = `https://jsonplaceholder.typicode.com/todos/${id}`

const getPostDetails = async () => {
    const response = await fetch(base_url)
    const data = await response.json()
    post.value = data
}

getPostDetails()
</script>

<template>
    <div class="d-flex justify-content-center align-items-center vh-100">
        <div class="card" style="width: 18rem;">
            <div class="card-body">
                <h5 class="card-title">{{ post.title }}</h5>
                <p class="card-text"><strong>Completado:</strong> {{ post.completed ? 'Sí' : 'No' }}</p>
                <p class="card-text"><strong>Id:</strong> {{ post.id }}</p>
                <RouterLink class="btn btn-success" to="/post">Regresar</RouterLink>
            </div>
        </div>
    </div>
</template>

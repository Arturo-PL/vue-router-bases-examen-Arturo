<script setup>
import { ref } from 'vue'
import { RouterLink } from 'vue-router'
import Loading from './components/Loading.vue'

const base_url = 'https://jsonplaceholder.typicode.com/todos'
const isLoading = ref(true)
const postList = ref([])

const getPosts = async () => {
    isLoading.value = true
    const response = await fetch(base_url)
    const data = await response.json()
    postList.value = data
    isLoading.value = false
}

getPosts()
</script>

<template>
    <Loading v-if="isLoading"/>
    <div v-else>
        <h3 style="color: #FFA500;">Lista de Publicaciones</h3>
        <template v-for="post in postList" :key="post.id">
            <RouterLink :to="`/post/${post.id}`">{{ post.title }}</RouterLink> <br />
        </template>
    </div>
</template>

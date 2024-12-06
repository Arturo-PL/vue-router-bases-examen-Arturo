<script setup>
import { RouterView, RouterLink } from 'vue-router';
</script>

<template>
  <ul class="nav justify-content-center">
    <li class="nav-item">
      <RouterLink to="/" class="nav-link active" aria-current="page">Home</RouterLink>
    </li>
    <li class="nav-item">
      <RouterLink to="/phone" class="nav-link">Phone</RouterLink>
    </li>
    <li class="nav-item">
      <RouterLink to="/movie" class="nav-link">Movie</RouterLink>
    </li>
    <li class="nav-item">
      <RouterLink to="/post" class="nav-link">Post</RouterLink>
    </li>
    <li class="nav-item">
      <RouterLink to="/tv" class="nav-link">Tv</RouterLink>
    </li>
  </ul>
  <div class="container">
    <RouterView />
  </div>
</template>


<style>
.menu {
  width: 300px;
  display: flex;
}

.link{
  margin-right: 10px;
}

.link:hover {
  color: white;
  background-color: #154c79 ;
  cursor: pointer;
}
</style>

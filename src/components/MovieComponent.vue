<!-- <script setup>
import { reactive } from 'vue';
import { items } from './movies.json'

const movies = reactive(items);
</script>

<template>
    <li v-for="(movie, index) in movies" :key="index" class="movie">
        <img :src="movie.image" :alt="movie.title" class="movie-image">
        <div class="text">
          <h2><b>{{ movie.name }}</b></h2>
          <p class="genre">{{ movie.genres.join(', ') }}</p>
          <p>{{ movie.description }}</p>
          <div class="rating">
            <span v-for="n in 5" :key="n" class="star">
              {{ n <= Math.round(movie.rating) ? '⭐️' : '' }} </span>
          </div>
        </div>
      </li>
</template>

<style>
p {
  color: #636363;
  font-size: 13px;
}

li {
  width: 33%;
  background: #FFFFFF;
  border-radius: 10px;''
}

span {
  background: #FFFFFF;
}

.movie-image {
  width: 100%;
  height: 420px;
  object-fit: cover;
  border-radius: 10px 10px 0 0;
}

.text {
  padding: 15px;
}

.genre {
  background-color: rgb(228, 228, 228);
  padding: 5px 5px 5px 10px;
  margin-top: 10px;
  margin-bottom: 10px;
  border-radius: 15px;
  font-weight: 500;
}

.rating {
  margin-top: 10px;
}

h2 {
  font-size: 28px;
}
</style> -->

<script setup>
const config = useRuntimeConfig();
const route = useRoute();
const { data: movie, pending, refresh } = await useFetch(`/movie/${route.params.id}?api_key=f62f750b70a8ef11dad44670cfb6aa57`,
  {
    baseURL: config.SERVER_URL,
    method: 'GET',
  }
);
const { data: casts } = await useFetch(`/movie/${route.params.id}/credits?api_key=f62f750b70a8ef11dad44670cfb6aa57`,
  {
    baseURL: config.SERVER_URL,
    method: 'GET',
  }
);

</script>

<template>
  <div v-if="!pending" class="max-w-5xl mx-auto p-2">
    <div class="flex items-center space-x-3 bg-blue-100 rounded-lg p-2">
      
      <h1 class="font-bold text-xl">{{ movie.title}}</h1>
    </div>
    <div class="flex shadow-md border rounded-lg mt-4">
      <img class="w-1/3 rounded-l-lg" :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path" alt="">
      <div class="flex flex-col w-2/3 p-8 justify-evenly">
        <div class="flex justify-between">
          <p class="font-semibold text-sm">Budget:</p>
          <p>{{ movie.budget }}</p>
        </div>
        <div class="flex justify-between">
          <p class="font-semibold text-sm">Revenue:</p>
          <p>{{ movie.revenue }}</p>
        </div>
        <div class="flex justify-between">
          <p class="font-semibold text-sm">Release Date:</p>
          <p>{{ movie.release_date }}</p>
        </div>
        <div class="flex justify-between">
          <p class="font-semibold text-sm">Run Time:</p>
          <p>{{ movie.runtime }}</p>
        </div>
        <div class="flex justify-between">
          <p class="font-semibold text-sm">Score:</p>
          <p>{{ movie.score }}</p>
        </div>
        <div class="flex justify-between">
          <p class="font-semibold text-sm">Genres:</p>
          <div class="flex space-x-3">
            <p v-for="genre in movie.genres" :key="genre.id">{{ genre.name }}</p>
          </div>
        </div>
        <div class="flex justify-between">
          <p class="font-semibold text-sm">IMDB Link:</p>
          <a class="text-blue-300 hover:text-blue-600" :href="'https://www.imdb.com/title/' + movie.imdb_id"
            target="_blank">Link</a>
        </div>
        <div class="flex justify-between">
          <p class="font-semibold text-sm">Homepage Link:</p>
          <a class="text-blue-300 hover:text-blue-600" :href="movie.homepage">Link</a>
        </div>
      </div>
    </div>
    <h1 class="font-bold text-lg mt-5">Overview</h1>
    <p>{{ movie.overview }}</p>
    <h1 class="font-bold text-lg mt-5">Credits</h1>
    <div class="grid grid-cols-6 text-sm gap-1">
      <p v-for="cast in casts.cast" :key="cast.id">
        {{ cast.name }}
      </p>
    </div>
  </div>
</template>
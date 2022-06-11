<script setup>
const config = useRuntimeConfig();
const route = useRoute();
// intial Database Call

const { data, error, pending, refresh } = await useFetch(() =>
    `/discover/movie?api_key=f62f750b70a8ef11dad44670cfb6aa57&page=${route.query.page}`,
    {
        baseURL: config.SERVER_URL,
        method: 'GET',
    });



const { data: g } = await useFetch(() => `/genre/movie/list?api_key=f62f750b70a8ef11dad44670cfb6aa57&language=en-US`,
    {
        baseURL: config.SERVER_URL,
        method: 'GET',
    });

function genreName(index) {
    return g.value.genres.filter(el => index === el.id).map(n => n.name).toString()
}
const search = () => {
    startDate.value = startInput.value
    endDate.value = endInput.value
    refresh()
}

</script>


<template>
    <NuxtLayout name="home">
        <div class="max-w-5xl mx-auto pt-20">
            <div v-if="!pending" class=" grid grid-cols-3 gap-3 pt-5">
                <NuxtLink :to="`${movie.id}`" class="bg-gray-200 rounded-lg border shadow-md hover:bg-blue-200"
                    v-for="(movie, index) in data.results" :key="index">
                    <div class="flex space-x-2 w-full">
                        <img class="w-2/5 rounded-l-lg" :src="'https://image.tmdb.org/t/p/w500/' + movie.poster_path"
                            alt="">
                        <div class="flex flex-col justify-between p-2">
                            <p class="text-sm font-semibold">{{ movie.original_title }}</p>
                            <div>
                                <p>{{ movie.release_date }}</p>
                                <div class="grid grid-cols-3 gap-2 text-xs break-normal">
                                    <p v-for="(genre, index2) of movie.genre_ids" :key="index2">
                                        {{ genreName(genre) }}
                                    </p>
                                </div>
                            </div>
                        </div>
                    </div>
                </NuxtLink>
            </div>
        </div>
        <Pagination class="mx-auto mt-6" :currentPage="data.page" :totalPages="data.total_pages" />
    </NuxtLayout>
</template>
<template>
    <div class="movie_detail">
        <div class="detail_top">
            <img :src="movie.poster_path" alt="">
            <div class="information">
                <h3><span>Title:</span>{{ movie.original_title }}</h3>
                <h3><span>Date:</span>{{ movie.release_date }}</h3>
                <h3><span>Time:</span>{{ movie.runtime }} mins</h3>
                <h3><span>Rating:</span>{{ movie.vote_average }}</h3>
                <h3><span>Budget:</span>{{ movie.budget }}</h3>
            </div>
        </div>
        <div class="overview">
            <p>{{ movie.overview }}</p>
        </div>
    </div>
</template>

<script>
import { ref, onBeforeMount } from "vue";
import { useRoute } from "vue-router";
import env from '@/env'

export default {
    setup() {
        const movie = ref({});
        const route = useRoute();
        const options = {
                method: 'GET',
                headers: {
                    'X-RapidAPI-Key': env.apiKey,
                    'X-RapidAPI-Host': 'advanced-movie-search.p.rapidapi.com'
                }
            };

        onBeforeMount(() => {
            fetch(`https://advanced-movie-search.p.rapidapi.com/movies/getdetails?movie_id=${route.params.id}`, options)
                .then(response => response.json())
                .then(data => {
                    movie.value = data;
                    console.log(movie.value)
                })
        })
        return {
            movie
        }
    }
}

</script>
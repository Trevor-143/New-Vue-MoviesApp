<template>
  <div class="home">
    <div class="featured_card">
      <router-link to="/movie/tt0409591">
        <img src="@/images/bleach.jpg" alt="bleach_poster" class="featured_img">
        <div class="details">
          <h3>Bleach</h3>
          <p>It follows the adventures of a teenager Ichigo Kurosaki, who inherits his parents' destiny after he obtains the powers of a Soul Reaper—a death personification similar to the Grim Reaper—from another Soul Reaper, Rukia Kuchiki.</p>
        </div>
      </router-link>
    </div>
    <form @submit.prevent="SearchMovies() " class="search_box">
      <input type="text" placeholder="search" v-model="search">
      <input type="submit" value="search">
    </form>

    <div class="movies_list">
      <div class="movie" v-for="movie in movies" :key="movie.id">
        {{ movie.original_title }}
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from "vue";
import env from "@/env";

export default {
  setup() {
    const search =ref('');
    const movies = ref([]);
    const SearchMovies = () => {
      if (search.value != '') {
        // console.log(search.value);
        const options = {
          method: 'GET',
          headers: {
            'X-RapidAPI-Key': env.apiKey,
            'X-RapidAPI-Host': 'advanced-movie-search.p.rapidapi.com'
          }
        };
        
        fetch(`https://advanced-movie-search.p.rapidapi.com/search/movie?query=${search.value}&page=1`, options)
          .then(response => response.json())
          .then(data => {
            movies.value = data.results;
            search.value = '';
            console.log(movies.value);
          });
          // .catch(err => console.error(err));
      }
    }

    return {
      search,
      movies,
      SearchMovies
    }
  }
}
</script>

<style>
  .featured_card {
    position: relative;
  }
  .featured_img {
    display: block;
    width: 100%;
    height: 300px;
    object-fit: cover;
    position: relative;
    z-index: 0;
  }
  .details {
    position: absolute;
    left: 0;
    right: 0;
    bottom: 0;
    background-image: linear-gradient(to top, rgba(0, 0, 0, 1), rgba(0, 0, 0, 0));
    padding: 20px;
    z-index: 1;
    color: #ffffff;

  }
  .details h3 {
    margin-bottom: 16px;
  }
  .search_box {
    display: flex;
    flex-direction: row;
    justify-content: flex-start;
    align-items: center;
    padding: 16px;
  }
  .search_box input {
    display: flex;
    appearance: none;
    border: none;
    outline: none;
    background: none;

  }
  .search_box input[type='text'] {
    width: 60%;
    color: #000000;
    background: rgba(255, 255, 255, 0.5);
    border: 2px solid rgba(255, 255, 255, 0);
    
    font-size: 20px;
    padding: 10px 16px;
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px;
    transition: 0.4s;
  }
  input::placeholder {
    color: #3f3f3f;
  }

  input[type='text']:focus {
    background: #000000;
    color: #ffffff;
    border: 2px solid rgba(255, 255, 255, 0.5);
  }
  .search_box input[type='submit'] {
    width: 100%;
    max-width: 100px;
    background: #ffffff;
    color: #000000;
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
    padding: 14px;
    font-size: 17px;
    text-transform: uppercase;
    transition: 0.4s;
  } 


</style>

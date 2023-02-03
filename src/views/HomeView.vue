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
        <router-link :to="'/movie/' + movie.id" class="movie_link">
          <img :src="movie.poster_path" alt="movie poster" class="product_img">
          <div class="detail">
            <div class="type"> {{ movie.vote_average }} </div>
            <h3>{{ movie.original_title }}</h3>
            <h4>{{ movie.release_date }}</h4>
          </div>
        </router-link>
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

<style scoped>
  .featured_card {
    position: relative;
  }
  .featured_img {
    display: block;
    width: 100%;
    height: 400px;
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
    justify-content: center;
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
    border-top-left-radius: 99px;
    border-bottom-left-radius: 99px;
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
    border-top-right-radius: 99px;
    border-bottom-right-radius: 99px;
    padding: 14px;
    font-size: 17px;
    text-transform: uppercase;
    transition: 0.4s;
  }
  .movies_list {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
  }
  .movie {
    display: flex;
    flex-direction: row;
    flex-wrap: wrap;
    position: relative;
  } 
  .movie_link {
    position: relative;
    height: 250px;
    width: 200px;
    margin: 15px;
  }
  .movie_link img {
    height: 250px;
    width: 200px;
    border-radius: 10px;
    object-fit: cover;
  }
  .detail {
    position: absolute;
    display: flex;
    flex-direction: column;
    padding: 10px;
    background-image: linear-gradient(to top, rgba(0, 0, 0, 1), rgba(0, 0, 0, 0));
    color: #fff;
    height: fit-content;
    bottom: 0;
    left: 0;
    right: 0;
  }
  .detail .type {
    padding: 15px;
    border-radius: 50%;
    width: 60px;
    height: 60px;
    display: flex;
    align-items: center;
    justify-content: center;
    background: #000;
    color: #fff;
  }



</style>

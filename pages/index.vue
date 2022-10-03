<template>
  <div class="home">
    <HeroSection />

    <div class="container movies">
      <div id="movie-grid" class="movie-grid">
        <div class="movie" v-for="(movie, index) in movies" :key="index">
          <div class="movie-img">
            <img
              :src="`https://image.tmdb.org/t/p/${movie.poster_path}`"
              alt=""
            />
            <p class="review">{{ movie.vote_average }}</p>
            <p class="overview">{{ movie.overview }}</p>
          </div>
          <div class="info">
            <p class="title">
              {{ movie.title.slice(0, 25)
              }}<span v-if="movie.title.length > 25">...</span>
            </p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'
import HeroSection from '../components/HeroSection.vue'

export default {
  name: 'IndexPage',
  components: { HeroSection },
  env: {
    api_key: process.env.API_KEY,
  },
  data() {
    return {
      movies: [],
    }
  },
  async fetch() {
    await this.getMovies()
  },
  methods: {
    async getMovies() {
      const data = axios.get(
        `https://api.themoviedb.org/3/movie/now_playing?api_key=${process.env.API_KEY}&language=en-US&page=1`
      )
      const result = await data
      this.movies = result.data.results
      console.log(this.movies)
    },
  },
}
</script>

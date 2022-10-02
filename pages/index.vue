<template>
  <div class="home">
    <HeroSection />
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

      return result
    },
  },
}
</script>

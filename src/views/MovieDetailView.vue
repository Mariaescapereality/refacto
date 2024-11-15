<template>
  <div class="details">
    <div 
      class="movie-ctn"
      :style="{ backgroundImage: `url(${movie.image})` }"
    >
      <div class="title">{{ movie.title }}</div>
    </div>    
  </div>
</template>

<script setup>
import { reactive, onMounted, ref } from 'vue';
import { useRoute } from 'vue-router';

const { params } = useRoute();
const { id: movieId } = params;

const movie = reactive({
  title: '',
  image: '',
  rank: null,
  description: '',
  trailer: ''
});

const fetchMovieDetails = async () => {
  try {
    const response = await fetch('datas/details/movies.json');
    const { movies } = await response.json();
    const foundMovie = movies.find(m => m.id === parseInt(movieId));

    if (foundMovie) {
      Object.assign(movie, foundMovie); 
    }
  } catch (error) {
    console.error('Error loading movie details:', error);
  }
};

onMounted(fetchMovieDetails);
</script>

<style scoped lang="scss">
.details {
  .title {
    position: relative;
    text-align: center;
    padding-top: 12%;
    font-size: 25px;
    z-index: 40;
  }

  .movie-ctn {
    height: 40vh;
    background-size: cover;
    background-position: center;
    position: relative;
    transition: background-image 0.3s ease-in-out; /* Added smooth transition */
  }

  .movie-ctn::after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    height: 40%;
    width: 100%;
    background: linear-gradient(0deg, rgba(2, 0, 36, 0) 0%, rgba(0, 0, 0, 0.7) 100%);
    z-index: 1;
  }
}
</style>



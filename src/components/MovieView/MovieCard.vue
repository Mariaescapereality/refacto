<template>
  <div class="movieCard" @click="goToMovie">
    <img :src="image" class="poster" alt="Movie Poster">
    <div class="title">
      {{ title }}
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';
import { useRouter } from 'vue-router';

// Définition des props
const props = defineProps({
  title: {
    type: String,
    default: ''
  },
  image: {
    type: String,
    default: '',
  },
  score: {
    type: Number,
    default: 2
  },
  id: {
    type: Number,
    default: 0
  }
});
const router = useRouter();
const goToMovie = () => {
  router.push(`/movie/${props.id}`);
};
</script>

<style scoped lang="scss">
.movieCard {
  margin-top: 40px;
  margin-bottom: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;

  img {
    height: 220px;
    width: 150px;
    border-radius: 6px;
    object-fit: cover; 
  }

  .title {
    margin-top: 10px;
    font-size: 18px;
    text-align: center;
  }
}
</style>

<template>
  <div class="slider-container">
    <button
      @click="scrollSlider(-150)"
      class="slider-scroll-button left"
      aria-label="Scroll left"
    >
      &#10094;
    </button>

    <div class="slider" ref="slider">
      <button
        v-for="(button, index) in buttons"
        :key="index"
        class="slider-button"
      >
        {{ button }}
      </button>
    </div>

    <button
      @click="scrollSlider(150)"
      class="slider-scroll-button right"
      aria-label="Scroll right"
    >
      &#10095;
    </button>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Liste des boutons de catégories
const buttons = [
  'Recommended', 'Action', 'Science-Fiction', 'Horror', 'Comedy', 'Drama'
];

// Référence du slider pour pouvoir manipuler son défilement
const slider = ref(null);

// Fonction générique pour faire défiler le slider à gauche ou à droite
const scrollSlider = (distance) => {
  if (slider.value) {
    slider.value.scrollBy({ left: distance, behavior: 'smooth' });
  }
};
</script>

<style scoped>
.slider-container {
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  width: 100%;
  overflow: hidden;
  padding: 0 16px;
}

.slider {
  display: flex;
  gap: 16px;
  padding: 0;
  overflow-x: auto;
  scroll-behavior: smooth;
  flex-wrap: nowrap;
  margin: 0;
}

.slider-button {
  padding: 10px 20px;
  background-color: #29304e;
  color: #95a8c5;
  border: none;
  font-size: 16px;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
  white-space: nowrap;
}

.slider-button:hover {
  background-color: #40506d;
}

.slider-scroll-button {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  background-color: #29304e;
  color: white;
  font-size: 24px;
  border: none;
  padding: 10px;
  cursor: pointer;
  border-radius: 50%;
  transition: background-color 0.3s;
  z-index: 1;
}

.slider-scroll-button:hover {
  background-color: #40506d;
}

.slider-scroll-button.left {
  left: 0;
}

.slider-scroll-button.right {
  right: 0;
}
</style>

<template>
  <div class="photo-gallery-container">
    <VueAgile>
      <img
        class="slide"
        v-for="(item, index) in images"
        :key="index"
        :src="require(`../assets/img/${item}`)"
      />
      <template slot="prevButton">
        <i class="fas fa-chevron-left">‹</i>
      </template>
      <template slot="nextButton">
        <i class="fas fa-chevron-right">›</i>
      </template>
    </VueAgile>
  </div>
</template>

<script>
import { VueAgile } from "vue-agile";

export default {
  name: "PhotoGallery",
  components: { VueAgile },
  props: { images: { type: Array } }
};
</script>

<style>
/* Agile controls */
.agile__list {
  background-color: #555;
  padding: 1em 0;
}

.agile__nav-button {
  background: transparent;
  border: none;
  color: #fff;
  cursor: pointer;
  font-size: 24px;
  height: 100%;
  position: absolute;
  top: 0;
  -webkit-transition-duration: 0.3s;
  transition-duration: 0.3s;
  width: 80px;
}
.agile__nav-button:hover {
  background-color: rgba(0, 0, 0, 0.2);
  opacity: 1;
}
.agile__nav-button--prev {
  left: 0;
}
.agile__nav-button--next {
  right: 0;
}
.agile__dots {
  bottom: -50px;
  left: 50%;
  position: absolute;
  -webkit-transform: translateX(-50%);
  transform: translateX(-50%);
}
.agile__dot {
  margin: 0 10px;
}
.agile__dot button {
  background-color: transparent;
  border: 1px solid #333;
  border-radius: 50%;
  cursor: pointer;
  display: block;
  height: 10px;
  font-size: 0;
  line-height: 0;
  margin: 0;
  padding: 0;
  -webkit-transition-duration: 0.3s;
  transition-duration: 0.3s;
  width: 10px;
}
.agile__dot--current button,
.agile__dot:hover button {
  background-color: #333;
}

.slide {
  display: block;
  height: 500px;
  object-fit: contain;
  width: 100%;
  max-height: 50vh;
}

.fas {
  font-style: normal;
  font-size: 3em;
}
</style>
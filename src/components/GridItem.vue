<template>
  <div class="grid-item">
    <img class="grid-item-thumb" :src="require(`../assets/img/${gridThumb}`)" />
    <div class="grid-item-text-overlay">{{gridTitle}}</div>
  </div>
</template>

<script>
export default {
  name: "GridItem",
  props: { gridTitle: { type: String }, gridThumb: { type: String } }
};
</script>

<style scoped>
.grid-item {
  width: 200px;
  height: 200px;
  cursor: pointer;
  transform: scale(1);
  transition: 0.3s transform;
  will-change: auto;
  overflow: hidden;
  position: relative;
  margin: 15px;
  border: 1px solid #ccc;
}

.grid-item:hover {
  transform: scale(1.1);
  border-color: rgba(255, 255, 255, 0);
}

.grid-item-thumb {
  width: 100%;
  height: auto;
  object-fit: cover;
}

.grid-item-text-overlay {
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  position: absolute;
  z-index: 2;
  background-color: rgba(0, 0, 0, 0.6);
  color: #fff;
  font-weight: bold;
  padding: 1em;
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: center;
  will-change: auto;
  transform: scale(1.3);
  transition: 0.3s all;
  opacity: 0;
}

.grid-item-text-overlay:hover {
  transform: scale(1);
  opacity: 1;
}
</style>
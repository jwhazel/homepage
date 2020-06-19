<template>
  <div class="project-details-container">
    <div class="project-details-inner">
      <section class="close-button-top-container">
        <span class="close-button-top" @click="$emit('close')">×</span>
      </section>

      <section>
        <h3 class="project-title">{{details.title}}</h3>
        <div class="pill-container">
          <span class="pill" v-for="(item, index) in tags" :key="index">{{item}}</span>
        </div>
      </section>

      <section>
        <PhotoGallery :images="images" />
      </section>

      <section class="description-container">
        <p v-for="(item, index) in description" :key="index">{{item}}</p>
      </section>

      <section class="link-container">
        <ul>
          <li v-if="details.url">
            <a :href="details.url" target="_blank">View the Project</a>
          </li>
          <li v-if="details.associated_link">
            <a :href="details.associated_link" target="_blank">Read the Story</a>
          </li>
          <li v-if="details.repo">
            <a :href="details.repo" target="_blank">See the Code</a>
          </li>
        </ul>
      </section>

      <section>
        <button @click="$emit('close')">
          <span class="close-x">×</span> Close
        </button>
      </section>
    </div>
  </div>
</template>

<script>
import PhotoGallery from "./PhotoGallery";

export default {
  name: "ProjectDetails",
  components: { PhotoGallery },
  props: { details: { type: Object } },
  computed: {
    images: function() {
      let imageArray = this.details.images.split(",").map(n => n.trim());
      return imageArray;
    },
    description: function() {
      let descriptionArray = this.details.description
        .split("||")
        .map(n => n.trim());
      return descriptionArray;
    },
    tags: function() {
      let tagsArray = this.details.tags.split(",").map(n => n.trim());
      return tagsArray;
    }
  }
};
</script>

<style scoped>
.project-details-container {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 999;
}

.project-details-curtain {
  background-color: rgba(0, 0, 0, 0.7);
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
}

.project-details-inner {
  background-color: #fff;
  padding: 2em 0em;
  position: absolute;
  width: 100%;
  height: 100%;
  overflow: scroll;
  box-sizing: border-box;
}

.pill-container {
  margin-bottom: 8px;
  margin-top: 20px;
}

.project-title {
  font-weight: 700;
  margin: 0;
  text-transform: uppercase;
  font-size: 2.5em;
  font-family: Montserrat, "Helvetica Neue", Helvetica, Arial, sans-serif;
}

.close-button-top-container {
  text-align: right;
  padding-right: 2em;
}

.close-button-top {
  font-size: 64px;
  line-height: 32px;
  font-weight: 100;
  cursor: pointer;
  transition: color 0.3s;
}

.close-button-top:hover {
  color: #ccc;
}

.close-x {
  font-family: arial, sans-serif;
  font-weight: bold;
  font-size: 16px;
  display: inline-block;
  vertical-align: middle;
}

.pill {
  font-weight: bold;
  font-size: 0.9em;
  color: #fff;
  background-color: #284c75;
  padding: 4px 12px;
  border-radius: 14px;
  margin: 0 10px;
}

.description-container {
  margin-top: 60px;
}

.link-container {
  margin: 30px 0;
}
li {
  display: inline-block;
  margin: 0 20px;
}
</style>
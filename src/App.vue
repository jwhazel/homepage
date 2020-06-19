<template>
  <div id="app">
    <main class="inner-content">
      <h1>
        <vue-typer
          :text="'Hello'"
          :repeat="0"
          initial-action="typing"
          :pre-type-delay="1000"
          :type-delay="200"
          :pre-erase-delay="2000"
          :erase-delay="1250"
          erase-style="select-all"
          :erase-on-complete="false"
          caret-animation="blink"
        ></vue-typer>
      </h1>
      <p>I'm Jesse Hazel. I'm a full stack developer in Louisville Kentucky. On top of writing code I also make interactive content, wrangle data, and build maps.</p>
      <section>
        <h2 class="subhead">Some of my work:</h2>
        <div class="grid-container">
          <GridItem
            v-for="(item, index) in portfolio"
            :key="index"
            :gridTitle="item.title"
            :gridThumb="item.thumb"
            @click.native="showItem(index)"
          />
        </div>
      </section>
      <!--
      <section>
        <h2 class="subhead">Some of my skills:</h2>
      </section>-->
    </main>
    <transition name="fade">
      <ProjectDetails
        v-if="detailsVisible"
        :details="projectDetails"
        @close="detailsVisible=false"
      />
    </transition>
  </div>
</template>

<script>
import GridItem from "./components/GridItem.vue";
import ProjectDetails from "./components/ProjectDetails.vue";
import { VueTyper } from "vue-typer";
import data from "./data/data.json";

export default {
  name: "App",
  components: { GridItem, ProjectDetails, VueTyper },
  data() {
    return {
      portfolio: data,
      detailsVisible: false,
      projectDetails: {}
    };
  },
  methods: {
    showItem: function(e) {
      this.projectDetails = this.portfolio[e];
      this.detailsVisible = true;
    }
  }
};
</script>

<style>
/* Keep the caret in vue-typer blinking */
.complete {
  display: inline-block !important;
}

/* Apply to #app when a modal is launched */
.noscroll {
  overflow: hidden;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  font-size: 1.1em;
}

.inner-content {
  max-width: 80vw;
  margin: 0 auto;
  padding: 0 10px;
  margin-top: 59px;
}

p {
  max-width: 500px;
  margin: 0 auto;
  text-align: left;
}

.main-header {
  background-color: #cfd8dc;
  padding: 1em;
  text-align: left;
  margin-bottom: 50px;
}

/*
.subhead {
  font-size: 1.2em;
  font-weight: bold;
  background-color: #284c75;
  color: #fff;
  display: inline-block;
  padding: 0.5em 1em;
  border-radius: 14px;
}
*/

.subhead {
  font-size: 1.2em;
  font-weight: bold;
  text-decoration: underline;
}

.grid-container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  animation-delay: 2s;
  animation-duration: 0.5s;
  animation-fill-mode: both;
}

@keyframes fade-in {
  from {
    opacity: 0;
    transform: translateX(20px);
  }
  to {
    opacity: 1;
    transform: translateX(0px);
  }
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s;
}
.fade-enter, .fade-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>

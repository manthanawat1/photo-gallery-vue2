<template>
  <div id="app">
    <Picture
      :picture="pictures[selectedPictureIndex]"
      :disabledButton="disabledButton"
      @show-previous="showPrevious"
      @show-next="showNext"
    />
    <Galleries
      :pictures="pictures"
      :selectedPictureIndex="selectedPictureIndex"
      @image-hover="handleImageHover"
    />
  </div>
</template>

<script lang="ts">
import { Component, Vue, Watch } from "vue-property-decorator";

import pictures from "./data";
import Picture from "./components/Picture.vue";
import Galleries from "./components/Galleries.vue";
import PicturesData from "./interfaces/Pictures";

@Component({
  components: {
    Picture,
    Galleries,
  },
})
export default class App extends Vue {
  pictures: PicturesData[] = [];
  disabledButton = "prev";
  selectedPictureIndex = 0;

  created() {
    this.pictures = pictures;
  }

  @Watch("selectedPictureIndex")
  handleSelectedPictureIndexChange(newValue: number) {
    if (newValue === 0) {
      this.disabledButton = "prev";
    } else if (newValue === this.pictures.length - 1) {
      this.disabledButton = "next";
    } else {
      this.disabledButton = "";
    }
  }

  handleImageHover(index: number) {
    this.selectedPictureIndex = index;
  }
  showPrevious() {
    if (this.selectedPictureIndex > 0) {
      this.selectedPictureIndex--;
    }
  }
  showNext() {
    if (this.selectedPictureIndex < this.pictures.length - 1) {
      this.selectedPictureIndex++;
    }
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Homemade+Apple&display=swap");

* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

html {
  font-size: 62.5%;
}

html,
body {
  height: 100%;
  margin: 0;
  background-color: #f6f7f8;
}

#app {
  font-family: "Homemade Apple", cursive;
  min-width: 300px;
  min-height: 300px;
  padding: 3rem;
  text-align: center;
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

@media (max-width: 60em) {
  html {
    font-size: 50%;
  }
}

@media (max-width: 37.5em) {
  html {
    font-size: 43.75%;
  }
}
</style>

<template>
  <div class="gallery-container" ref="galleryContainer">
    <img
      v-for="(picture, index) in pictures"
      :src="picture.link"
      :key="index"
      :alt="picture.title"
      @mouseover="handleImageHover(index)"
      :class="{ 'hover-image': index === clickedIndex }"
    />
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import PicturesData from "../interfaces/Pictures";

export default Vue.extend({
  props: {
    pictures: {
      type: Array as () => PicturesData[],
      required: true,
      default: () => [],
    },
    selectedPictureIndex: {
      type: Number,
      required: true,
    },
  },
  data() {
    return {
      clickedIndex: 0,
    };
  },
  watch: {
    selectedPictureIndex(newValue) {
      this.clickedIndex = newValue;
      this.scrollingPicture();
    },
  },
  methods: {
    handleImageHover(index: number) {
      this.clickedIndex = index;
      this.$emit("image-hover", index);
    },
    scrollingPicture() {
      const container = this.$refs.galleryContainer as HTMLElement;
      const widthPicture = container.querySelector("img")?.clientWidth || 0;
      const scrollAmount = this.clickedIndex * (widthPicture + 14);
      container.scrollTo({ left: scrollAmount, behavior: "smooth" });
    },
  },
});
</script>

<style scoped>
.gallery-container {
  margin: 2rem auto auto auto;
  max-width: 110rem;
  width: 100%;
  height: 10.5rem;
  overflow: hidden;
  transition: all 0.3s ease-in-out !important;
  display: flex;
  gap: 14px;
}

img {
  width: 14rem;
  height: 100%;
  border: 4px solid;
  border-image: repeating-linear-gradient(
      to bottom right,
      #9fa5a9,
      #c1c7cb,
      #e5e7e9,
      #c1c7cb,
      #9fa5a9
    )
    20;
  transition: all 0.2s ease-in-out;
}

img:hover,
.hover-image {
  width: 14rem;
  height: 100%;
  border: 4px solid;
  padding: 4px;
  border-image: linear-gradient(45deg, #f3ed46, #ff8c00) 10;
}
</style>

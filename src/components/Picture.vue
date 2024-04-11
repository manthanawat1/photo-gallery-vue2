<template>
  <div class="image-container">
    <img :src="picture.link" :alt="picture.title" />
    <button
      :disabled="disabledButton === 'prev'"
      class="btn btn--left"
      :class="disabledButton !== 'prev' ? 'hover-button' : 'disable-btn'"
      @click="handleClick('prev')"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="3"
        stroke="currentColor"
        class="btn-icon"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M15.75 19.5L8.25 12l7.5-7.5"
        />
      </svg>
    </button>
    <button
      :disabled="disabledButton === 'next'"
      class="btn btn--right"
      :class="disabledButton !== 'next' ? 'hover-button' : 'disable-btn'"
      @click="handleClick('next')"
    >
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke-width="3"
        stroke="currentColor"
        class="btn-icon"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          d="M8.25 4.5l7.5 7.5-7.5 7.5"
        />
      </svg>
    </button>

    <div class="detail-text-container">
      <p class="title-text">{{ picture.title }}</p>
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import PicturesData from "../interfaces/Pictures";

export default Vue.extend({
  props: {
    picture: {
      type: Object as () => PicturesData,
      required: true,
    },
    disabledButton: {
      type: String,
    },
  },
  methods: {
    handleClick(status: string) {
      if (status === "prev") {
        this.$emit("show-previous");
      } else {
        this.$emit("show-next");
      }
    },
  },
});
</script>

<style scoped>
.image-container {
  margin: auto auto 0 auto;
  position: relative;
  max-width: 110rem;
  width: 100%;
  height: calc(100vh - 30rem);
  transition: all 0.3s ease-in-out !important;
  box-shadow: -3px -3px 6px rgba(0, 0, 0, 0.03),
    6px 6px 25px rgba(0, 0, 0, 0.15);
}

img {
  width: 100%;
  height: 100%;
  overflow: hidden;
  object-fit: cover;
  box-shadow: 0 4px 4px -2px rgba(0, 0, 0, 0.25);
  transition: all 0.4s ease-in-out;
}

.btn {
  transition: all 0.3s ease-in-out !important;
  background-color: rgba(#000000, 0.05);
  border: 2px solid #838383;
  border-radius: 50%;
  height: 4rem;
  width: 4rem;
  position: absolute;

  display: flex;
  align-items: center;
  justify-content: center;

  top: 50%;
}

.btn::before {
  border-bottom: 0.7rem solid #313132;
  border-left: 1.5rem solid transparent;
}

.btn--left {
  left: 0;
  transform: translate(-50%, -50%);
}

.btn--right {
  right: 0;
  transform: translate(50%, -50%);
}

.btn-icon {
  height: 2rem;
  width: 2rem;
  stroke: #838383;
}

.hover-button:hover {
  background-color: #838383 !important;
  box-shadow: -3px -3px 6px rgba(0, 0, 0, 0.03),
    6px 6px 25px rgba(0, 0, 0, 0.15);
}

.hover-button:hover > .btn-icon {
  cursor: pointer;
  stroke: #fff;
  transform: scaleY(1.2);
  transition: all 0.2s ease-in-out;
}

.disable-btn {
  opacity: 0 !important;
}

.detail-text-container {
  position: absolute;
  bottom: 0rem;
  background: rgba(0, 0, 0, 0.3);
  backdrop-filter: blur(5px);
}

.detail-text-container > p {
  color: #fff;
  padding: 0rem 2rem;
  text-align: left;
}

.title-text {
  font-size: 1.5rem;
  font-weight: 500;
}

@media (max-height: 40.625em) {
  .image-container {
    height: calc(100vh - 15rem);
  }
}
</style>

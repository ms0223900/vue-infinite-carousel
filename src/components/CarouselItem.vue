<template>
  <div class="carousel-item" :style="style">
    <img
      :alt="singleImgData.name"
      :src="singleImgData.src"
    />
  </div>
</template>

<script>
export default {
  name: 'CarouselItem',
  props: {
    singleImgData: {
      name: String,
      src: String,
      posKey: Number,
    },
  },
  computed: {
    style() {
      const {
        posKey,
      } = this.singleImgData;
      const zIndex = posKey === 0 ? 10 : -1;
      const transform = `translateX(${posKey * 100}%)`;
      return ({
        zIndex,
        transform,
      });
    },
  },
};
</script>

<style scoped>
  .carousel-item {
    display: flex;
    align-items: center;
    position: absolute;
    left: 0px;
    top: 0px;
    bottom: 0px;
    width: 100%;
    margin: auto;
    transition: all 0.3s ease-in-out;
  }
  .carousel-item img {
    display: block;
    width: 100%;
  }
</style>

<template>
  <div class="carousel-list">
    <button class="carousel-btn left" @click="$emit('update-left-shift')">{{ '＜' }}</button>
    <carousel-item
      v-for="(imgData, i) in imgListData"
      :key="i"
      :singleImgData="imgData"
    />
    <button class="carousel-btn right" @click="$emit('update-right-shift')">{{ '＞' }}</button>
  </div>
</template>

<script>
import CarouselItem from './CarouselItem.vue';

export default {
  components: { CarouselItem },
  name: 'CarouselList',
  props: {
    imgListData: Array,
  },
  emits: [
    'update-left-shift',
    'update-right-shift',
  ],
};
</script>

<style scoped>
  .carousel-list {
    position: relative;
    display: flex;
    align-items: center;
    width: 100%;
    padding-top: 60%;
    border-radius: 8px;
    overflow: hidden;
  }
  .carousel-btn {
    position: absolute;
    z-index: 100;
    top: 0px;
    bottom: 0px;
    margin: auto;
    padding: 20px 4px;
    /* max-height: 40px; */
    border: none;
    cursor: pointer;
    background-color: #333;
    color: #fff;
  }
  .carousel-btn:hover {
    background-color: #888;
  }
  .carousel-btn.left {
    left: 0px;
  }
  .carousel-btn.right {
    right: 0px;
  }
</style>

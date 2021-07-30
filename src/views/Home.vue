<template>
  <div class="home">
    <carousel-list-container :imgList="imgList" :shiftInterval="3" :autoShift="true" />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import HelloWorld from '@/components/HelloWorld.vue'; // @ is an alias to /src
import CarouselListContainer from '@/containers/CarouselListContainer.vue';

export default defineComponent({
  name: 'Home',
  components: {
    CarouselListContainer,
  },
  data() {
    return ({
      imgList: [
        'https://via.placeholder.com/300x300',
        'https://via.placeholder.com/400x400',
        'https://via.placeholder.com/500x500',
        'https://via.placeholder.com/600x600',
        'https://via.placeholder.com/700x700',
      ],
    });
  },
});
</script>
<style scoped>
  .home {
    max-width: 720px;
    margin: auto;
  }
</style>

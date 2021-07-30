<template>
  <div class="carousel-wrapper">
    <carousel-list
      :imgListData="imgListData"
      @update-left-shift="handleUpdateImgPosKey('add')"
      @update-right-shift="handleUpdateImgPosKey('minus')"
    />
  </div>
</template>
<script lang="ts">
import CarouselList from '@/components/CarouselList.vue';
import { defineComponent, PropType } from 'vue';

const minusKey = (key = -1, maxKey = 1) => {
  if (key === -1) return maxKey;
  return key - 1;
};
const addKey = (key = -1, maxKey = 1) => {
  if (key === maxKey) return -1;
  return key + 1;
};
const convertImgList = (imgList: string[]) => {
  let filledImgList = [...imgList];
  if (imgList.length === 1) {
    filledImgList = [
      ...imgList,
      ...imgList,
      ...imgList,
    ];
  }
  if (imgList.length === 2) {
    filledImgList = [...imgList, ...imgList];
  }
  const lastIdx = filledImgList.length - 1;
  return ([
    {
      posKey: -1,
      name: 'pic',
      src: filledImgList[lastIdx],
    },
    ...filledImgList.slice(0, lastIdx).map((img, i) => ({
      posKey: i,
      name: 'pic',
      src: img,
    })),
  ]);
};

export default defineComponent({
  components: { CarouselList },
  name: 'CarouselListContainer',
  props: {
    imgList: Array as PropType<any[]>,
    shiftInterval: Number as PropType<number>,
    autoShift: {
      type: Boolean as PropType<boolean>,
      default: true,
    },
  },
  data() {
    return ({
      timer: -Infinity,
      imgListData: convertImgList(this.imgList || []),
    });
  },
  methods: {
    handleUpdateImgPosKey(minusOrAdd = 'minus') {
      const maxKey = this.imgListData.length - 2;
      const newImgListData = minusOrAdd === 'minus' ? (
        this.imgListData.map((img) => ({ ...img, posKey: minusKey(img.posKey, maxKey) }))
      ) : (
        this.imgListData.map((img) => ({ ...img, posKey: addKey(img.posKey, maxKey) }))
      );
      this.imgListData = newImgListData;
      clearInterval(this.timer);
      this.handleUpdateImgPosKeyIntervally();
    },
    handleUpdateImgPosKeyIntervally() {
      if (this.shiftInterval && this.autoShift) {
        this.timer = setInterval(() => {
          this.handleUpdateImgPosKey('minus');
        }, this.shiftInterval * 1000);
      }
    },
  },
  mounted() {
    this.handleUpdateImgPosKeyIntervally();
  },
});
</script>
<style scoped>
  .carousel-wrapper {
    /* position: relative; */
  }
</style>

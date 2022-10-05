<template>
  <swiper class="detail-swiper">
    <swiper-item v-for="item in image">
      <img :src="item"/>
    </swiper-item>
  </swiper>
</template>

<script>
import {Swiper,SwiperItem} from '@/components/common/swiper'
export default {
  name: "DetailSwiper",
  components:{
    Swiper,
    SwiperItem
  },
  props:{
    image:{
      type:Array,
      default(){
        return []
      }
    }
  }
}
</script>

<style scoped>
  .detail-swiper {
    height: 350px;
  }
</style>
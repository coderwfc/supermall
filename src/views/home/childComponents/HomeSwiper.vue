<template>
  <Swiper class="swiper_nav">
    <SwiperItem v-for="item in banner">
      <a :href="item.link">
        <img :src="item.image" @load="swiperImgLoad">
      </a>
    </SwiperItem>
  </Swiper>
</template>

<script>
import {Swiper,SwiperItem} from '@/components/common/swiper'
export default {
  name: "HomeSwiper",
  props:{
    banner:{
      type:Array,
      default(){
        return []
      }
    }
  },
  components:{
    Swiper,
    SwiperItem
  },
  data(){
    return{
      isload:false
    }
  },
  methods:{
    swiperImgLoad(){
      if (!this.isload){
        this.$emit('swiperImgLoad')
        this.isload = true
      }

    }
  }
}
</script>

<style scoped>
  .swiper_nav {
    margin-top: 44px;
  }
</style>
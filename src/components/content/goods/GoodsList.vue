<template>
  <div class="goodsList">
    <goods-item v-for="item in list" :item="item"></goods-item>
  </div>
</template>

<script>
import GoodsItem from "@/components/content/goods/GoodsItem";
export default {
  name: "GoodsList",
  components:{
    GoodsItem
  },
  props:{
    list:{
      type:Array,
      default(){
        return []
      }
    }
  }
}
</script>

<style scoped>
.goodsList {
  display: flex;
  flex-wrap: wrap;
  width: 100%;
  justify-content: space-evenly;
}
</style>
<template>
  <div class="goodsItem" @click="itemclick">
    <img :src="item.show.img" @load="imgload">
    <div class="goodsInfo">
      <p>{{item.title}}</p>
      <span class="price">{{item.price}}</span>
      <img src="@/assets/img/home/collect.png">
      <span class="collect">{{item.cfav}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "GoodsItem",
  props:{
    item:{
      type:Object,
      default(){
        return {}
      }
    }
  },
  methods:{
    imgload(){
      this.$bus.$emit('itemImgload')
    },
    itemclick(){
      this.$router.push('/detail/' + this.item.iid)
    }
  }
}
</script>

<style scoped>
.goodsItem {
  width: 48%;
  padding: 5px;
}
.goodsItem>img {
  width: 100%;
}
.goodsInfo {
  text-align: center;
}
.goodsInfo p {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}
.goodsInfo img {
  width: 20px;
  vertical-align:text-bottom;
}
.price {
  color: var(--color-high-text);
  padding-right: 5px;
}
</style>
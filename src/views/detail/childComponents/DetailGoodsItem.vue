<template>
  <div v-if="Object.keys(detailInfo).length !== 0" id="detailInfo">
    <div class="key">{{detailInfo.detailImage[0].key}}</div>
    <div class="item">
      <img v-for="item in detailInfo.detailImage[0].list" :src="item" @load="detailImgLoad">
    </div>
  </div>
</template>

<script>
export default {
  name: "DetailGoodsItem",
  props:{
    detailInfo:{
      type:Object,
      default(){
        return {}
      }
    }
  },
  methods:{
    detailImgLoad(){
      this.$emit('detailImgLoad')
    }
  }
}
</script>

<style scoped>
  #detailInfo {
    margin-top: 30px;
    padding: 0 8px;
  }
  .key {
    margin: 0 auto;
    background-color:#cbdee4;
    width: fit-content;
    border-radius: 25%;
    padding: 10px;
  }
  .item>img {
    width: 100%;
  }
</style>
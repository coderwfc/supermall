<template>
  <div v-if="Object.keys(goods).length !== 0" class="base">
    <div class="title">{{goods.title}}</div>
    <div class="price">
      <span class="newPrice">{{goods.newPrice}}</span>
      <span  v-if="goods.oldPrice" class="oldPrice">{{goods.oldPrice}}</span>
    </div>
    <div class="columns">
      <span class="sell">{{goods.columns[0]}}</span>
      <span class="collect">{{goods.columns[1]}}</span>
      <span class="delivery">
        <img :src="goods.services[goods.services.length-1].icon" width="20px">
        {{goods.services[goods.services.length-1].name}}
      </span>
    </div>
    <div class="service">
      <span class="delay">{{goods.services[0].name}}</span>
      <span class="backfee">
        <img :src="goods.services[1].icon" width="20px">
        {{goods.services[1].name}}
      </span>
      <span class="hold">
        <img :src="goods.services[2].icon" width="20px">
        {{goods.services[2].name}}
      </span>
    </div>
  </div>
</template>

<script>
export default {
  name: "DetailData",
  props:{
   goods:{
     type:Object,
     default(){
       return {}
     }
   }
  }
}
</script>

<style scoped>
  .base {
    margin-top: 15px;
    padding: 0 8px;
    color: #9999;
  }
  .title {
    font-size: 18px;
    color: #222;
    line-height: inherit;
  }
  .price {
    margin-top: 10px;
  }
  .newPrice {
    font-size: 24px;
    color: var(--color-high-text);
    margin-right: 10px;
  }
  .oldPrice {
    font-size: 15px;
    text-decoration: line-through;
  }
  .columns {
    font-size: 14px;
    margin-top: 15px;
    display: flex;
    border-bottom: 3px solid #f2f5f8;
  }
  .sell {
    flex: 1;
  }
  .collect {
    flex: 1;
  }
  .delivery{
    flex: 1;
  }
  .delivery>img {
    vertical-align: text-bottom;
  }
  .service {
    height: 40px;
    font-size: 14px;
    color:#222222;
    margin-top: 20px;
    display: flex;
    border-bottom: 5px solid #f2f5f8;
  }
  .delay {
    flex: 1;
  }
  .backfee {
    flex: 1;
  }
  .backfee>img {
    vertical-align: text-bottom;
  }
  .hold {
    flex: 1;
  }
  .hold>img {
    vertical-align: text-bottom;
  }
</style>
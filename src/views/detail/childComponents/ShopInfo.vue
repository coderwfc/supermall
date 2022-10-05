<template>
  <div id="shopinfo" v-if="Object.keys(info).length !== 0">
    <div class="logo">
      <img :src="info.logo">
      <span>{{info.name}}</span>
    </div>

    <div class="sellInfo">
      <div class="sells">
        {{info.sells}}
        <p>总销量</p>
      </div>
      <div class="goodsCount">
        {{info.goodsCount}}
        <p>全部宝贝</p>
      </div>
      <div class="fans">
        {{info.fans}}
        <p>粉丝数</p>
      </div>

      <div class="item">
        <div v-for="item in info.score" class="itemDetail">
          <span class="itemname">{{item.name}}</span>
          <span class="score" :class="{itemscore:item.isBetter}">{{item.score}}</span>
          <span class="low" :class="{hightOrLow:item.isBetter}">{{item.isBetter ? '高':'低'}}</span>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: "ShopInfo",
  props:{
    info:{
      type:Object,
      default(){
        return {}
      }
    }
  }
}
</script>

<style scoped>
  #shopinfo {
    margin-top: 30px;
    padding: 0 8px;
  }
  .logo > img{
    width:80px;
    border-radius: 50%;
    vertical-align: middle;
  }
  .logo>span {
    font-size: 18px;
    color: #5c6b77;
    margin-left: 20px;
  }
  .sellInfo {
    margin-top: 30px;
    display: flex;
  }
  .sells {
    flex: 1;
    margin-top: 18px;
    font-size: 18px;
    font-weight: bold;
    color: #222222;
    text-align: center;
  }
  .sells > p {
    margin-top: 13px;
    font-size: 14px;
    font-weight: normal;
    color: #000;
  }
  .goodsCount {
    flex: 1;
    margin-top: 18px;
    font-size: 18px;
    font-weight: bold;
    color: #222222;
    text-align: center;
  }
  .goodsCount > p {
    margin-top: 13px;
    font-size: 14px;
    font-weight: normal;
    color: #000;
  }
  .fans {
    flex: 1;
    margin-top: 18px;
    border-right: 2px solid lightgray;
    font-size: 18px;
    font-weight: bold;
    color: #222222;
    text-align: center;

  }
  .fans > p{
    margin-top: 13px;
    font-size: 14px;
    font-weight: normal;
    color: #000;
  }
  .item {
    flex: 2;
    margin-left: 20px;
  }
  .itemDetail {
    margin-top: 8px;
    position: relative;
  }
  .itemname {
    font-size: 14px;
    margin-right: 15px;
  }
  .score {
    color: green;
  }
  .itemscore {
    color: var(--color-high-text);
  }
  .low {
    color: green;
    position: absolute;
    top: 0;
    left: 110px;
    bottom: 0;

  }
  .hightOrLow {
    color:var(--color-high-text);
    position: absolute;
    top: 0;
    left: 110px;
    bottom: 0;
  }
</style>
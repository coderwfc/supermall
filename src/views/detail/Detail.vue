<template>
  <div id="detail">
    <detail-nav-bar class="bar"/>
    <scroll class="wrapper" ref="scroll">
      <detail-swiper :image="images"/>
      <detail-data :goods="goods"/>
      <shop-info :info="shop"/>
      <detail-goods-item :detailInfo="detailInfo" @detailImgLoad="imgdata"/>
      <ul>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
        <li></li>
      </ul>
    </scroll>
  </div>
</template>

<script>
import DetailNavBar from "@/views/detail/childComponents/DetailNavBar";
import DetailSwiper from "@/views/detail/childComponents/DetailSwiper";
import DetailData from "@/views/detail/childComponents/DetailData";
import ShopInfo from "@/views/detail/childComponents/ShopInfo";
import Scroll from "@/components/common/scroll/Scroll";
import DetailGoodsItem from "@/views/detail/childComponents/DetailGoodsItem";

import {getDetailData,Goods,Shop} from "@/network/detail";
import {debounce} from "@/utils/debounce";
export default {
  name: "Detail",
  data(){
    return{
      iid:null,
      images:[],
      goods:{},
      shop:{},
      detailInfo:{}
    }
  },
  created() {
    this.iid = this.$route.params.iid
    getDetailData(this.iid).then((res)=>{
      console.log(res);
      const data = res.result
      this.images = data.itemInfo.topImages
      this.goods = new Goods(data.itemInfo,data.columns,data.shopInfo.services)
      this.shop = new Shop(data.shopInfo)

      this.detailInfo = data.detailInfo
    })
  },
  components:{
    DetailNavBar,
    DetailSwiper,
    DetailData,
    ShopInfo,
    Scroll,
    DetailGoodsItem
  },
  methods:{
    imgdata(){
      this.$refs.scroll.refresh()
    }
  }
}
</script>

<style scoped>
  #detail {
    height: 100vh;
    position: relative;
    z-index: 10;
    background-color: #ffffff;
  }
  .wrapper {
    height: calc(100% - 44px);
  }
  .bar {
    position: relative;
    z-index: 10;
    background-color: #ffffff;
  }
</style>
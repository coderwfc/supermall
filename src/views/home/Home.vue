<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物街</div>
    </nav-bar>
    <TabControl :title="['流行','新款','精选']"  @tabClick="tabClick"
                class="tabcontrol" v-show="isfixed" ref="tabcontrol2"/>
    <scroll class="scroll" ref="scroll"
            :probe-type="3" @hideOr="hideOrClick"
            :pull-up-load="true" @pullUpLoad="update">
    <HomeSwiper :banner="banner" @swiperImgLoad="swiperImgLoad"/>
    <HomeRecommend :recommend="recommend"/>
    <HomeView/>
    <TabControl :title="['流行','新款','精选']"  @tabClick="tabClick" ref="tabcontrol1" v-show="istabbar"/>
    <GoodsList :list="goods[currentType].list"/>
    </scroll>
    <back-top @click.native="topclick" v-show="isShow"/>

  </div>
</template>

<script>
import NavBar from "@/components/common/navbar/NavBar";
import TabControl from "@/components/content/tabControl/TabControl";
import GoodsList from "@/components/content/goods/GoodsList";
import Scroll from "@/components/common/scroll/Scroll";
import BackTop from "@/components/content/backtop/BackTop";

import HomeSwiper from "@/views/home/childComponents/HomeSwiper";
import HomeRecommend from "@/views/home/childComponents/HomeRecommend";
import HomeView from "@/views/home/childComponents/HomeView";

import {getHomeMultidata,getHomeGoods} from "@/network/home";
import {debounce} from "@/utils/debounce";


export default {
  name: "Home",
  components: {
    NavBar,
    HomeSwiper,
    HomeRecommend,
    HomeView,
    TabControl,
    GoodsList,
    Scroll,
    BackTop
  },
  data(){
    return{
      banner:[],
      recommend:[],
      goods:{
        'pop':{page:0,list:[]},
        'new':{page:0,list:[]},
        'sell':{page:0,list:[]}
      },
      currentType:'pop',
      isShow:false,
      getOffsetTop:0,
      isfixed:false,
      istabbar:true,
      saveY:0
    }
  },
  created() {
    this.getHomeMultidata()

    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
  },
  mounted() {
    const refresh = debounce(this.$refs.scroll.refresh(),500)
    this.$bus.$on('itemImgload',()=>{
      // console.log('....');
      refresh()
    })
  },
  activated() {
    this.$refs.scroll.scrollTo(0,this.saveY,0)
    this.$refs.scroll.refresh()
  },
  deactivated() {
    this.saveY = this.$refs.scroll.getsaveY()
  },
  methods:{
    tabClick(index){
      switch (index){
        case 0:
          this.currentType = 'pop'
          break
        case 1:
          this.currentType = 'new'
          break
        case 2:
          this.currentType = 'sell'
          break
      }
      this.$refs.tabcontrol1.currentIndex = index
      this.$refs.tabcontrol2.currentIndex = index

    },
    topclick(){
      this.$refs.scroll.scrollTo(0,0,500)
    },
    hideOrClick(position){
      this.isShow =  (-position.y) > 1000

      if ((-position.y) >= this.getOffsetTop){
        this.isfixed = true
        this.istabbar = false
      }else {
        this.isfixed = false
        this.istabbar = true
      }

    },
    update(){
      // console.log('上拉加载');
      this.getHomeGoods(this.currentType)
      // this.$refs.scroll.scroll.refresh()
    },
    swiperImgLoad(){
      // console.log(this.$refs.tabcontrol1.$el.offsetTop);
      this.getOffsetTop = this.$refs.tabcontrol1.$el.offsetTop
    },
    // 网络请求方法
    getHomeMultidata(){
      getHomeMultidata().then(res => {
        this.banner = res.data.banner.list
        this.recommend = res.data.recommend.list
      })
    },
    getHomeGoods(type){
      const page = this.goods[type].page + 1
      getHomeGoods(type,page).then(res => {
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1

        this.$refs.scroll.scroll.finishPullUp()
      })
    }

  }
}
</script>

<style scoped>
  #home {
    height: 100vh;
    position: relative;
  }
  .tabcontrol {
    margin-top: 44px;
    position: relative;
    z-index: 10;
  }
  .home-nav {
    background-color: var(--color-tint);
    color: white;
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    z-index: 10;
  }
  .scroll {
    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
  }
</style>

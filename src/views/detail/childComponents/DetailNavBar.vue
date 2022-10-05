<template>
  <NavBar>
    <div slot="left" class="left" @click="backclick">
      <img src="@/assets/img/detail/back.png">
    </div>
    <div slot="center" class="center">
      <div v-for="(item,index) in title" class="item"  @click="itemclick(index)"
           :class="{active:currentIndex === index}">{{item}}</div>
    </div>
  </NavBar>
</template>

<script>
import NavBar from "@/components/common/navbar/NavBar";
export default {
  name: "DetailNavBar",
  components:{
    NavBar
  },
  data(){
    return {
      title:['商品','参数','评论','推荐'],
      currentIndex:0,
    }
  },
  methods:{
    backclick(){
      this.$router.go(-1)
    },
    itemclick(index){
      this.currentIndex = index
    }
  }
}
</script>

<style scoped>
  .center {
    display: flex;
    font-size: 13px;
  }
  .left>img {
    width: 25px;
    margin-top: 10px;
  }
  .item {
    flex: 1;
  }
  .active {
    color: var(--color-high-text);
  }
</style>
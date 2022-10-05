<template>
  <div class="homeRecommend">
    <div v-for="item in recommend" class="recommendItem">
      <a :href="item.link">
        <img :src="item.image">
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "HomeRecommend",
  props:{
    recommend:{
      type:Array,
      default(){
        return []
      }
    }
  }
}
</script>

<style scoped>
  .homeRecommend {
    display: flex;
    width: 100%;
    font-size: 12px;
    text-align: center;
    padding: 15px 0 30px;
    border-bottom: 10px solid #e9e9e9;
  }
  .recommendItem {
    flex: 1;
  }
  .recommendItem img {
    width: 100%;
    margin-bottom: 10px;
  }
</style>
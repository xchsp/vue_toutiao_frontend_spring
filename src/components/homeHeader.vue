<template>
  <div class="header">
    <span class="iconfont iconnew"></span>
    <div @click="$router.push('/search')" class="search">
      <span class="iconfont iconsearch"></span>
      搜索新闻
    </div>
    <span @click="$router.push('/profile')" class="iconfont iconwode"></span>
  </div>
</template>

<script>
export default {}
</script>

<style lang="less" scoped>
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 2.778vw;
  height: 13.611vw;
  background-color: #ff0000;
  color: #fff;
}
.search {
  width: 58.333vw;
  height: 9.444vw;
  line-height: 9.444vw;
  text-align: center;
  border-radius: 4.722vw;
  margin: 0 auto;
  background-color: rgba(242, 242, 242, 0.5);
}
.iconnew {
  font-size: 54px;
}
.iconwode {
  font-size: 20px;
}
</style>
<template>
  <div class="head">
    <div @click="$router.back()" class="left">
      <span class="iconfont iconjiantou2"></span>
      <span class="iconfont iconnew"></span>
    </div>
    <span @click="follow" class="follow" v-if="!post.has_follow">关注</span>
    <span @click="unfollow" class="alfollow" v-if="post.has_follow">已关注</span>
  </div>
</template>

<script>
export default {
  props: ['post'],
  methods: {
    follow() {
      this.$axios({
        url: '/user_follows/' + this.post.user.id,
        method: 'GET'
      }).then(res => {
        console.log(res)
        const { message } = res.data
        if (message == '关注成功') {
          this.post.has_follow = true
        }
      })
    },
    unfollow() {
      this.$axios({
        url: '/user_unfollow/' + this.post.user.id,
        method: 'GET'
      }).then(res => {
        console.log(res)
        const { message } = res.data
        if (message == '取消关注成功') {
          this.post.has_follow = false
        }
      })
    }
  }
}
</script>

<style lang="less" scoped>
.head {
  padding: 0 2.778vw;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .left {
    display: flex;
    align-items: center;
    .iconjiantou2 {
      font-size: 15px;
    }
    .iconnew {
      font-size: 54px;
    }
  }
  .follow {
    width: 16.111vw;
    height: 2.222vw;
    padding: 2.222vw 1.111vw;
    line-height: 2.222vw;
    text-align: center;
    font-size: 12px;
    background-color: #f00;
    color: #fff;
    border-radius: 4.444vw;
  }
  .alfollow {
    width: 16.111vw;
    height: 2.222vw;
    padding: 2.222vw 1.111vw;
    line-height: 2.222vw;
    text-align: center;
    font-size: 12px;
    background-color: #eee;
    color: #888;
    border-radius: 4.444vw;
  }
}
</style>
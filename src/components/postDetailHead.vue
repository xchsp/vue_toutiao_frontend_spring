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

<script type="text/ecmascript-6">
export default {
  props: ['post'],
  methods: {
    follow() {
      console.log(this.post)
      this.$axios({
        url: '/user_follows/' + this.post.userid,
        method: 'GET'
      }).then(res => {
        console.log(res)
        const { message } = res.data
        if (message == '关注成功') {
          this.post.has_follow = true
        }
        else{
          this.$toast.fail(message)
        }
      })
    },
    unfollow() {
      this.$axios({
        url: '/user_follows/' + this.post.userid,
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
    padding: 0 10/@vv;
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
      width: 58/@vv;
      height: 8/@vv;
      padding: 8/@vv 4/@vv;
      line-height: 8/@vv;
      text-align: center;
      font-size: 12px;
      background-color: #f00;
      color: #fff;
      border-radius: 16/@vv;
    }
    .alfollow {
      width: 58/@vv;
      height: 8/@vv;
      padding: 8/@vv 4/@vv;
      line-height: 8/@vv;
      text-align: center;
      font-size: 12px;
      background-color: #eee;
      color: #888;
      border-radius: 16/@vv;
    }
  }
</style>

<template>
  <div>
    <headerMiddle title="我的关注"></headerMiddle>
    <div :key="index" class="item" v-for="(item,index) of fllowList">
      <img :src="item.picPath" alt class="avatar" />
      <div class="itemMiddle">
        <div class="name">{{item.nickname}}</div>
        <div class="time">2019-10-10</div>
      </div>
      <div @click="cancelFllow(item.id)" class="btnCancel">取消关注</div>
    </div>
  </div>
</template>

<script>
import headerMiddle from '@/components/HeaderMiddle'
export default {
  components: {
    headerMiddle
  },
  data() {
    return {
      fllowList: {}
    }
  },
  methods: {
    getData() {
      this.$axios({
        url: '/user_follows/',
        method: 'GET'
      }).then(res => {
        this.fllowList = res.data
        console.log(this.fllowList)
        this.fllowList.forEach(element => {
          if (!element.picPath) {
            element.picPath = '/static/imgs/default.png'
          } else {
            element.picPath = this.$axios.defaults.baseURL.replace("/api","") + element.picPath
          }
        })
      })
    },
    cancelFllow(id) {
      this.$axios({
        url: '/user_follows/' + id,
        method: 'GET'
      }).then(res => {
        console.log(res)
        this.getData()
      })
    }
  },
  mounted() {
    this.getData()
  }
}
</script>

<style lang="less" scoped>
.item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 5.556vw;
  border-bottom: 1px solid #eee;
}
.avatar {
  width: 11.111vw;
  border-radius: 50%;
}
.itemMiddle {
  flex: 1;
  padding-left: 2.778vw;
}
.time {
  color: #888;
  font-size: 14px;
}
.btnCancel {
  height: 8.333vw;
  line-height: 8.333vw;
  padding: 0 2.778vw;
  color: #888;
  font-size: 14px;
  background-color: #eee;
  border-radius: 5.556vw;
}
</style>

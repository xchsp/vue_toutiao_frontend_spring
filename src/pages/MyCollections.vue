<template>
  <div class="container">
    <headerMiddle title="我的收藏" />

    <post :key="index" :post="item" v-for="(item,index) of collectionsList"></post>
    <!-- <van-loading class="loading" color="#1989fa" size="24px" type="spinner" /> -->
  </div>
</template>

<script>
import headerMiddle from '@/components/HeaderMiddle'
import post from '@/components/post'

export default {
  components: {
    headerMiddle,
    post
  },
  data() {
    return {
      collectionsList: []
    }
  },
  methods: {
    getData() {
      this.$axios({
        url: '/user_star',
        method: 'GET'
      }).then(res => {
        console.log(res.data)
        this.collectionsList = res.data
        // this.collectionsList = res.data.data
        // this.collectionsList.forEach(element => {
        //   // 每一个收藏都是一个 element
        //   element.comment_length = element.comments.length
        //   element.cover.forEach(element => {
        //     if (element.url.indexOf('http') < 0) {
        //       element.url = this.$axios.defaults.baseURL + element.url
        //     }
        //   })
        // })
      })
    }
  },
  mounted() {
    this.getData()
    // setTimeout(() => {
    //   this.getData()
    // }, 500)
  }
}
</script>

<style lang="less" scoped>
.singleCover {
  display: flex;
  padding: 5.556vw;
  border-bottom: 1px solid #eee;
  .left {
    width: 66%;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    padding: 0 2.778vw 0 0;
    .info {
      margin-top: 5.556vw;
      color: #888;
      font-size: 14px;
    }
  }
  .right {
    width: 34%;
    height: 20.556vw;
    overflow: hidden;
    img {
      width: 100%;
      height: auto;
      object-fit: cover;
    }
  }
}
.multipCover {
  padding: 5.556vw;
  border-bottom: 1px solid #eee;
  .cover {
    display: flex;
    justify-content: space-between;
    margin-top: 2.778vw;
    .imgWrapper {
      width: 32%;
      height: 20.556vw;
      overflow: hidden;
      img {
        width: 100%;
        height: auto;
        object-fit: cover;
      }
    }
  }
  img {
    width: 31.111vw;
    height: 20.556vw;
  }
}
</style>

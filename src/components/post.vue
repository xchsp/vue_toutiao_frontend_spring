

<template>
  <div>
    <!-- 视频播放器模板 -->
    <div class="videoPost" v-if="post.type ==2">
      <div @click="toPostDetail" class="title">{{post.title}}</div>
      <div @click="toPostDetail" class="cover">
        <img alt class="imgRight" v-lazy="$fixImgUrl(post.cover[0].url)" />
        <div class="btnPlay">
          <span class="iconfont iconshipin"></span>
        </div>
      </div>
      <div class="info">{{post.nickname}} {{post.comment_length}}跟帖</div>
    </div>

    <div class="single" v-else-if="post.cover.length >0 && post.cover.length <3">
      <div class="left">
        <div @click="toPostDetail" class="title">{{post.title}}</div>
        <div class="info">{{post.nickname}} {{post.comment_length}}跟帖</div>
      </div>
      <img @click="toPostDetail" class="imgRight" v-lazy="$fixImgUrl(post.cover[0].url)" />
    </div>

    <div class="multip" v-else-if="post.cover.length >=3">
      <div @click="toPostDetail" class="title">{{post.title}}</div>
      <div class="cover">
        <!-- <img :src="post.cover[0].url" alt />
        <img :src="post.cover[1].url" alt />
        <img :src="post.cover[2].url" alt />-->
        <!-- 实现懒加载 -->
        <img
          :key="index"
          @click="toPostDetail"
          alt
          v-for="(img,index) in 3"
          v-lazy="$fixImgUrl(post.cover[index].url)"
        />
      </div>
      <div class="info">{{post.nickname}} {{post.comment_length}}跟帖</div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['post'],
  methods: {
    toPostDetail() {
      this.$router.push({
        name: 'postDetailPage',
        params: {
          id: this.post.id
        }
      })
    }
  }
}
</script>

<style lang="less" scoped>
.single {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 2.778vw;
  border-bottom: 1px solid #eee;
  .left {
    flex: 1;
    height: 20.833vw;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    .title {
      display: -webkit-box;
      -webkit-box-orient: vertical;
      -webkit-line-clamp: 2;
      overflow: hidden;
    }
    .info {
      color: #888;
      font-size: 14px;
    }
  }
  .imgRight {
    width: 33.611vw;
    height: 20.833vw;
    object-fit: cover;
  }
}
.multip {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 2.778vw;
  border-bottom: 1px solid #eee;
  .title {
    flex: 1;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;
    overflow: hidden;
  }
  .info {
    color: #888;
    font-size: 3.889vw;
  }
  .cover {
    margin: 2.778vw 0;
    img {
      width: 32%;
      height: 20.833vw;
      margin-right: 1.111vw;
      object-fit: cover;
    }
  }
}
.videoPost {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  padding: 2.778vw;
  border-bottom: 1px solid #eee;
  .title {
    flex: 1;
    display: -webkit-box;
    -webkit-box-orient: vertical;
    -webkit-line-clamp: 2;
    overflow: hidden;
  }
  .info {
    color: #888;
    font-size: 3.889vw;
  }
  .cover {
    position: relative;
    margin: 2.778vw 0;
    .btnPlay {
      position: absolute;
      top: 0;
      left: 0;
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: center;
      align-items: center;
      .iconshipin {
        width: 15.278vw;
        height: 15.278vw;
        line-height: 15.278vw;
        border-radius: 50%;
        text-align: center;
        background: #ccc;
        color: #fff;
        font-size: 40px;
      }
    }
    img {
      width: 100%;
      height: 47.222vw;
      object-fit: cover;
    }
  }
}
</style>

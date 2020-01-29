<template>
  <div>
    <headerMiddle title="个人中心" />
    <div class="profile">
      <img :src="profile.picPath" @click="$router.push('/editProfile')" alt class="avatar" />
      <div class="profile-middle">
        <div>
          <span class="iconfont iconxingbienan" v-if="profile.sex ==1"></span>
          <span class="iconfont iconxingbienv" v-else></span>
          {{profile.nickname}}
        </div>
        <div class="time">2019-10-10</div>
      </div>
      <span class="iconfont iconjiantou1"></span>
    </div>
    <cellBar @click="$router.push('/myFllow')" desc="关注的用户" label="我的关注"></cellBar>
    <cellBar @click="$router.push('/myComments')" desc="我的跟帖" label="跟帖/回复"></cellBar>
    <cellBar @click="$router.push('/myCollections')" desc="我的收藏" label="文章/视频"></cellBar>
    <cellBar @click="$router.push('/tabManager')" label="栏目管理"></cellBar>
    <cellBar @click="$router.push('/editProfile')" label="设置"></cellBar>
    <cellBar @click="$router.replace('/login')" label="退出"></cellBar>
  </div>
</template>

<script>
import headerMiddle from '@/components/HeaderMiddle'

import cellBar from '@/components/cellBar'
export default {
  data() {
    return {
      profile: {}
    }
  },
  components: {
    cellBar,
    headerMiddle
  },
  methods: {
    getData() {
      this.$axios({
        url: '/user/' + localStorage.getItem('user_id'),
        method: 'GET'
      }).then(res => {
        this.profile = res.data
        console.log(this.profile.picPath)
        if (!this.profile.picPath) {
          // this.profile.picPath = '/static/imgs/default.png'
          this.profile.picPath =
            'https://p3.pstatp.com/list/190x124/pgc-image/Rft0hGGCLk6YgJ'
        } else {
          this.profile.picPath =
            this.$axios.defaults.baseURL.replace("/api","") + this.profile.picPath
            console.log(this.profile.picPath)
        }
      })
    }
  },
  mounted() {
    this.getData()
  }
}
</script>

<style lang="less" scoped>
.profile {
  display: flex;
  align-items: center;
  padding: 11.111vw 0;
  border-bottom: 1.389vw solid #eee;
}
.avatar {
  margin-left: 5.556vw;
  width: 70 / 360 * 100vw;
  height: 70 / 360 * 100vw;
  border-radius: 50%;
}
.profile-middle {
  flex: 1;
  padding: 0 5.556vw;
  font-size: 3.889vw;
}
.iconxingbienan {
  margin: 0 1.111vw;
  color: skyblue;
}
.time {
  margin-top: 1.111vw;
  font-size: 3.889vw;
}
</style>

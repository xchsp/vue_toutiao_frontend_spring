<template>
  <div>
    <headerMiddle title="编辑资料"></headerMiddle>
    <div class="avatar">
      <img :src="profile.picPath" alt class="avatar-img" />
      <van-uploader :after-read="afterRead" />
      <!--<van-uploader :after-read="afterRead" class="uploadFile" />-->
    </div>
    <cellBar :desc="profile.nickname" @click="isShowNickname=true" label="昵称"></cellBar>
    <cellBar @click="isShowPwd=true" desc="******" label="密码"></cellBar>
    <cellBar :desc="profile.sex" @click="isShowGender=true" label="性别"></cellBar>

    <van-dialog
      @confirm="editProfile({nickname:newNickname})"
      show-cancel-button
      title="编辑昵称"
      use-slot
      v-model="isShowNickname"
    >
      <van-field focus="true" placeholder="请输入用户名" v-model="newNickname" />
    </van-dialog>

    <van-dialog
      @confirm="editProfile({password:newPwd})"
      show-cancel-button
      title="编辑密码"
      use-slot
      v-model="isShowPwd"
    >
      <van-field focus="true" placeholder="请输入密码" type="password" v-model="newPwd" />
    </van-dialog>

    <van-action-sheet
      :actions="genderList"
      @select="selectGender"
      cancel-text="取消"
      v-model="isShowGender"
    />
  </div>
</template>

<script>
import headerMiddle from '@/components/HeaderMiddle'
import cellBar from '@/components/cellBar'
export default {
  data() {
    return {
      profile: {},
      isShowNickname: false,
      isShowPwd: false,
      isShowGender: false,

      newNickname: '',
      newPwd: '',
      genderList: [{ name: '男' }, { name: '女' }]
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
          this.profile.picPath =
            'https://p3.pstatp.com/list/190x124/pgc-image/Rft0hGGCLk6YgJ'
        } else {
          this.profile.picPath =
            this.$axios.defaults.baseURL.replace("/api","") + this.profile.picPath
          console.log(this.profile.picPath)
        }
        this.profile.sex = this.profile.sex == 0 ? '女' : '男'
      })
    },
    editProfile(newData) {
      this.$axios({
        url: '/user_update/' + localStorage.getItem('user_id'),
        method: 'POST',
        headers: {
          Authorization: localStorage.getItem('token')
        },
        data: newData
      }).then(res => {
        this.getData()
        console.log(res)
      })

    },
    selectGender(event) {
      console.log(event.name)
      this.editProfile({ gender: event.name == '男' ? 1 : 0 })
      this.isShowGender = false
    },
    afterRead(file) {
      console.log('afterRead')
      const data = new FormData()
      data.append('file', file.file)
      this.$axios({
        url: '/upload',
        method: 'POST',
        data
      }).then(res => {
        console.log(res.data)
        console.log(res.data.data.url)
        this.editProfile({ picPath: res.data.data.url })
      })
    }
  },
  mounted() {
    this.getData()
  }
}
</script>

<style lang="less" scoped>

  .avatar {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px;
    position: relative;

    .avatar-img {
      display: block;
      width: 100/@vv;
      height: 100/@vv;
      border-radius: 50%;
    }
    // 修改元素的大小
    /deep/.van-uploader__upload {
      width: 100/@vv;
      height: 100/@vv;
    }
    /deep/.van-uploader {
      position: absolute;
      left: 50%;
      top: 50%;
      transform: translate(-50%, -50%);
      opacity: 0;
    }
  }
</style>

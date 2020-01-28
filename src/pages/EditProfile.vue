<template>
  <div>
    <headerMiddle title="编辑资料"></headerMiddle>
    <div class="avatar">
      <img :src="profile.head_img" alt class="avatar-img" />
      <van-uploader :after-read="afterRead" class="uploadFile" />
    </div>
    <cellBar :desc="profile.nickname" @click="isShowNickname=true" label="昵称"></cellBar>
    <cellBar @click="isShowPwd=true" desc="******" label="密码"></cellBar>
    <cellBar :desc="profile.gender" @click="isShowGender=true" label="性别"></cellBar>

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
        this.profile = res.data.data
        if (!this.profile.head_img) {
          this.profile.head_img =
            'https://p3.pstatp.com/list/190x124/pgc-image/Rft0hGGCLk6YgJ'
        } else {
          this.profile.head_img =
            this.$axios.defaults.baseURL + this.profile.head_img
        }
        this.profile.gender = this.profile.gender == 0 ? '女' : '男'
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
        console.log(res)
      })
      this.getData()
    },
    selectGender(event) {
      console.log(event.name)
      this.editProfile({ gender: event.name == '男' ? 1 : 0 })
      this.isShowGender = false
    },
    afterRead(file) {
      const data = new FormData()
      data.append('file', file.file)
      this.$axios({
        url: '/upload',
        method: 'POST',
        data
      }).then(res => {
        console.log(res.data)
        this.editProfile({ head_img: res.data.data.url })
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
  padding: 8.333vw;
  text-align: center;
  position: relative;
}
.avatar-img {
  width: 19.444vw;
  border-radius: 50%;
}
.uploadFile {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  opacity: 0;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
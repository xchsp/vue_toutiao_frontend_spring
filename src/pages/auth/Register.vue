<template>
  <div class="container">
    <div class="closeBtn">
      <span @click="$router.back()" class="iconfont iconjiantou2"></span>
    </div>
    <div class="logo">
      <span class="iconfont iconnew"></span>
    </div>
    <div class="inputName">
      <authInput
        @input="setUserName"
        err_message="请输入正确的手机号"
        placeholder="用户名/手机号"
        rule="^\d{5,10}$"
        type="text"
      ></authInput>
    </div>
    <div class="inputNickName">
      <authInput
        @input="setNickName"
        err_message="请输入正确的昵称"
        placeholder="昵称"
        rule="^\w{5,10}$"
        type="text"
      ></authInput>
    </div>
    <div class="inputPwd">
      <authInput
        @input="setPassword"
        err_message="请输入正确的密码"
        placeholder="请输入密码"
        rule="^\d{3,10}$"
        type="password"
      ></authInput>
    </div>
    <div class="btn">
      <authBtn @click="sendRegister" text="注册" />
    </div>
  </div>
</template>

<script>
import authInput from '@/pages/auth/components/authInput'
import authBtn from '@/pages/auth/components/authBtn'
export default {
  data() {
    return {
      username: '',
      password: '',
      nickname: ''
    }
  },
  components: {
    authInput,
    authBtn
  },
  methods: {
    setUserName(name) {
      this.username = name
    },
    setNickName(name) {
      this.nickname = name
    },
    setPassword(password) {
      this.password = password
    },
    sendRegister() {
      this.$axios({
        url: '/register',
        method: 'POST',
        data: {
          username: this.username,
          email: this.nickname,
          password: this.password
        }
      }).then(res => {
        console.log(res)
        if (res.data.statusCode && res.data.statusCode == 400) {
          this.$toast.fail(res.data.message)
        } else {
          this.$toast.success(res.data.message)
        }
      })
    }
  }
}
</script>

<style lang="less" scoped>
.container {
  padding: 5.556vw;
}
.closeBtn {
  .iconfont {
    font-size: 7.5vw;
  }
}
.logo {
  display: flex;
  justify-content: center;
  .iconfont {
    color: #d81e06;
    font-size: 35vw;
  }
}
.btn {
  margin: 50px auto 0;
}
</style>

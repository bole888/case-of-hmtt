<template>
  <div id="login">
    <div class="container">
      <div class="close">
        <span class="iconfont iconicon-test"></span>
      </div>
      <div class="logo">
        <span class="iconfont iconnew"></span>
      </div>
      <div class="inputs">
        <hminput
          placeholder="请输入手机号/用户名"
          class="input"
           msg='用户名或者手机号输入不正确'
          :rules="/^(\d{5,6})$|^(1\d{10})$/"
          v-model="users.username"
        ></hminput>
        <hminput
          placeholder="请输入密码"
          class="input"
          type="password"
          v-model="users.password"
          :rules="/^\S{3,16}$/"
           msg='请输入3-16位的密码'
        ></hminput>
      </div>
      <p class="tips">
        没有账号？
        <a href="#/register" class>去注册</a>
      </p>
      <hmbutton @click="login">登陆</hmbutton>
    </div>
  </div>
</template>

<script>
import hmbutton from '@/components/hmbutton.vue'
import hminput from '@/components/hminput.vue'
import { login } from '@/apis/user.js'

export default {
  data () {
    return {
      users: {
        password: '123456',
        username: '10086'
      }
    }
  },
  components: {
    hmbutton, hminput
  },

  methods: {
    async login () {
      if (/^(\d{5,6})$|^(1\d{10})$/.test(this.users.username) &&
     /^\S{3,16}$/.test(this.users.password)) {
        let res = await login(this.users)
        console.log(res)
        if (res.data.message === '用户不存在') {
          this.$toast.fail(res.data.message)
        } else {
          localStorage.setItem('hm_token', res.data.data.token)
          localStorage.setItem('hm_users', JSON.stringify(res.data.data.user))
          this.$router.push({ name: 'personal' })
        }
      } else {
        this.$toast.fail('用户数据输入不合法')
      }
    }
  }
}
</script>

<style lang='less' scoped>
.container {
  padding: 20px;
}

.close {
  span {
    font-size: 27 / 360 * 100vw;
  }
}

.logo {
  display: flex;
  justify-content: center;

  span {
    display: block;
    font-size: 126 / 360 * 100vw;
    color: #d81e06;
  }
}

.inputs {
  input {
    margin-bottom: 20px;
  }
}

.tips {
  text-align: right;
  margin-bottom: 20px;

  a {
    color: #3385ff;
  }
}
</style>

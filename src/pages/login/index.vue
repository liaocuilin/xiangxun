<template>
  <div class="login_pages" ref="login">
      <div class="login_title">
        基于物联网的主动发光标志牌远程控制系统
      </div>
      <div class="login_form">
        <div class="login_usename">
          <div class="_name">
            用户名：
          </div>
          <div class="_field">
            <input type="text" placeholder="" v-model="account">
          </div>
        </div>
        <div class="login_usename">
          <div class="_name">
            密码：
          </div>
          <div class="_field">
            <input type="password" placeholder="" v-model="password">
          </div>
        </div>
        <div class="login_btn" @click="login()">
          登录
        </div>
      </div>
      <div class="login_footer">
        © 湖南湘旭交安光电高科技股份有限公司
      </div>
  </div>
</template>

<script>
// import axios from 'axios'
import md5 from 'md5'
export default {
  name: 'login',
  components: {
  },
  data() {
    return {
      clientHeight: '',
      account: 'ceshi001',
      password: '123456'
    }
  },
  created() {
  },
  mounted() {
    this.clientHeight = `${document.documentElement.clientHeight}`;
    window.onresize = function getCurHeight() {
      this.clientHeight = `${document.documentElement.clientHeight}`;
    }
  },
  watch: {
      clientHeight: function () {
        this.changeFixed(this.clientHeight)
      }
    },
  methods:{
    changeFixed(clientHeight){
      this.$refs.login.style.height = clientHeight+'px';
    },
    login () {
      let {account, password} = this
      let params = {
        account,
        password: md5(password)
      }
      this.$store.dispatch("LoginAdmin", params).then(res => {
        if (res) {
          this.$router.push('main')
        }
      })
    }
  }
}
</script>
<style lang="scss" scoped>
@import '@/assets/styles/login.scss';
</style>
<template>
  <div class="page-login">
    <div class="login-header">
      <a
        class="logo"
        href="/"
      ></a>
    </div>
    <div class="login-panel">
      <div class="banner">
        <img
          alt="美团网"
          height="370"
          src="//s0.meituan.net/bs/file/?f=fe-sso-fs:build/page/static/banner/www.jpg"
          width="480"
        />
      </div>
      <div class="form">
        <h4
          class="tips"
          v-if="error"
        >
          <i />
          {{error}}
        </h4>
        <p>
          <span>账号登录</span>
        </p>
        <el-input
          prefix-icon="profile"
          v-model="username"
        ></el-input>
        <el-input
          prefix-icon="password"
          type="password"
          v-model="password"
        ></el-input>
        <div class="foot">
          <el-checkbox v-model="checked">7天内自动登录</el-checkbox>
          <a>忘记密码？</a>
        </div>
        <el-button
          @click="login"
          class="btn-login"
          size="mini"
          type="success"
        >登录</el-button>
        <p>
          还没有账号？
          <a
            href="/register"
            target="_top"
          >免费注册</a>
        </p>
      </div>
    </div>
  </div>
</template>

<script>
import CryptoJS from "crypto-js";
export default {
  data() {
    return {
      checked: "",
      username: "",
      password: "",
      error: ""
    };
  },
  layout: "blank",
  methods: {
    login() {
      this.$axios
        .post("/users/signin", {
          username: encodeURIComponent(this.username),
          password: CryptoJS.MD5(this.password).toString()
        })
        .then(({ status, data }) => {
          if (status === 200) {
            if (data && data.code === 0) {
              location.href = "/";
            } else {
              this.error = data.msg;
            }
          } else {
            this.error = `服务器出错`;
          }
        });
    }
  }
};
</script>

<style lang='scss'>
@import "@/assets/css/login/index.scss";
</style>

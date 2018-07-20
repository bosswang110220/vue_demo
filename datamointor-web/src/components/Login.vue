<template>
	<div id="login">
		 <div class="site-content">
		<el-form :model="loginForm" :rules="loginRules">
			<h2>数据监测平台登录</h2>
			<el-form-item prop="username">
				<el-input v-model="loginForm.username" name="username" placeholder="请输入用户名/手机号" auto-complete="on"></el-input>
			</el-form-item>

			<el-form-item prop="password">
				<el-input v-model="loginForm.password" name="password" placeholder="请输入密码" auto-complete="on"></el-input>
			</el-form-item>

			<el-form-item>
				<el-button type="primary" @click="handleLogin">登录</el-button>
			</el-form-item>
		</el-form>
		 </div>
	</div>
</template>

import { loginReq } from '@/apis/Login'

<script>
export default {
  name: "#login",
  data() {
    return {
      loginForm: {
        username: "",
        password: ""
      },
      loginRules: {
        username: [
          {
            required: true,

            message: "请输入用户名",

            trigger: "blur"
          }
        ],
        password: [
          {
            required: true,
            message: "请输入密码",
            trigger: "blur"
          }
        ]
      }
    };
  },
  methods: {
    handleLogin() {
      this.$refs.loginForm.validate(valid => {
        if (valid) {
          loginReq(this.loginForm.username, this.loginForm.password).then(
            res => {
              console.log(res.data.status);
            }
          );
        } else {
          console.log("用户名或密码错误");
        }
      });
    }
  }
};
</script>
<style scoped>
.el-input {
  width: 300px;
 
}

.site-content {
  min-height: 100%;
  padding: 13rem 68rem 30px 30px;
}
</style>
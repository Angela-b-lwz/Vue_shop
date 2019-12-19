<template>
  <div class="login_container">
      <div class="login_box">
        <!-- 头像区域 -->
        <div class="avatar_box">
          <img src="../assets/logo.png" alt="">
        </div>
        <!-- 登录表单区域 -->
          <el-form ref="loginFormRef" class="login_form" :model="loginForm" :rules="loginFormRules">
            <el-form-item prop="username">
              <el-input  prefix-icon="iconfont icon-users" v-model="loginForm.username"></el-input>
            </el-form-item>
            <el-form-item prop="password">
              <el-input type="password" prefix-icon="iconfont icon-3702mima" v-model="loginForm.password"></el-input>
            </el-form-item>
            <el-form-item class="btns">
              <el-button type="primary" @click="login">登录</el-button>
              <el-button type="info" @click="resetLogin">重置</el-button>
            </el-form-item>
          </el-form>
      </div>
  </div>
</template>

<script>
export default {
  data () {
    return {
      loginForm: { username: 'admin', password: '123456' },
      loginFormRules: { username: [ { required: true, message: '请输入用户名', trigger: 'blur' }, { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' } ],
      password: [ { required: true, message: '请输入密码', trigger: 'blur' }, { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' } ] } }
  },
  created () {
  },
  methods: {
    // 重置功能调用表单resetFields()方法对整个表单进行重置，将所有字段值重置为初始值并移除校验结果
    resetLogin() { this.$refs.loginFormRef.resetFields() },
    login() {
      this.$refs.loginFormRef.validate(valid => {
         if (!valid) return
        this.$http.post('login', this.loginForm )          
     })
    }
   }
}
</script>

<style lang="less" scoped>
.login_container {
  background-color: #2b4b6b;
  height: 100%;
}
.login_box {
  position: absolute;
  top: 50%;
  left: 50%;
  transform: translate(-50%,-50%);
  width: 450px;
  height: 300px;
  border-radius: 3px;
  background-color: #fff;
  .avatar_box {
    height: 130px;
    width: 130px;
    border: 1px solid #eee;
    border-radius: 50%;
    padding: 10px;
    box-shadow: 0 0 10px #ddd;
    position: absolute;
    left: 50%;
    transform: translate(-50%, -50%);
    background-color: #fff;
    img {
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background-color: #eee;
    }
  }
}
.login_form {
  position: absolute;
  bottom: 0;
  width: 100%;
  padding: 0 20px;
  box-sizing: border-box;
}
.btns {
  display: flex;
  justify-content: flex-end;
}
</style>

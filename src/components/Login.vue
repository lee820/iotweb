<template>
    <div class="login_container">
        <div class="login_box">
            <h1>Login</h1>
            <el-form ref="loginFormRef" label-width="80px" :model="LoginForm" :rules="rules" class="login_form">
                <el-form-item label="用户名:" prop="username">
                    <el-input v-model="LoginForm.username"></el-input>
                </el-form-item>
                <el-form-item label="密码:" prop="password">
                    <el-input type="password" v-model="LoginForm.password"></el-input>
                </el-form-item>
                <el-form-item class="login_btns">
                    <el-button type="primary" @click="login">登录</el-button>
                    <el-button type="info" @click="resetLoginForm">重置</el-button>
                </el-form-item>
            </el-form>
        </div>
    </div>
</template>

<script>
export default {
  data () {
    return {
      LoginForm: {
        username: 'lee',
        password: '112233'
      },
      rules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 16, message: '长度在3到16个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 6, max: 16, message: '长度在6到16个字符', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    resetLoginForm () {
      this.$refs.loginFormRef.resetFields()
    },
    login () {
      this.$refs.loginFormRef.validate((valid) => {
        if (!valid) {
          this.$message.error('登录失败')
          return
        }
        // axios使用form表单提交数据
        this.$http({
          method: 'post',
          url: '/auth',
          data: this.LoginForm,
          transformRequest: [function (data) {
            let ret = ''
            for (const it in data) {
              ret += encodeURIComponent(it) + '=' + encodeURIComponent(data[it]) + '&'
            }
            return ret
          }],
          headers: {
            'Content-Type': 'application/x-www-form-urlencoded'
          }
        }).then((res) => {
          // 1. 将登录成功后的token，保存到客户端的sessionStorage中
          console.log(res)
          window.sessionStorage.setItem('token', res.data.Data)
          this.$message.success('登录成功')
          this.$router.push('/home')
        }).catch(error => {
          console.log(error)
        })
      })
    }
  }
}
</script>

<style scoped>
.login_container {
    background-color: #2d4d6d;
    height: 100%;
}

.login_box {
    width: 450px;
    height: 300px;
    background-color: #ffffff;
    border-radius: 3px;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
}

.login_box h1 {
    position: absolute;
    left: 50%;
    transform: translate(-50%);
}

.login_btns {
    display: flex;
    float: right;
}

.login_form {
    position: absolute;
    bottom: 0;
    padding: 20px;
    width: 100%;
    box-sizing: border-box;
}
</style>

<template>
  <div class="login">
    <div class="login-wrap">
      <el-form
        :model="ruleForm"
        status-icon
        :rules="rules"
        ref="ruleForm"
        label-width="100px"
        class="login-form"
      >
        <el-form-item label="用户名" prop="username">
          <el-input
            placeholder="请输入用户名"
            v-model="ruleForm.username"
          ></el-input>
        </el-form-item>
        <el-form-item label="密码" prop="password">
          <el-input
            placeholder="请输入密码"
            type="password"
            v-model="ruleForm.password"
            autocomplete="off"
          ></el-input>
        </el-form-item>

        <el-form-item class="login-submit">
          <el-button
            class="login-submit-btn"
            type="primary"
            @click="submitForm('ruleForm')"
            >登录</el-button
          >
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>
<script>
export default {
  name: "login",
  data() {
    var validateUsername = (rule, value, callback) => {
      if (value !== "0" && !value) {
        return callback(new Error("请输入用户"));
      }
      callback();
    };
    var validatePass = (rule, value, callback) => {
      if (value !== "0" && !value) {
        callback(new Error("请输入密码"));
      } else {
        callback();
      }
    };

    return {
      ruleForm: {
        username: "",
        password: ""
      },
      rules: {
        username: [{ validator: validateUsername, trigger: "change" }],
        password: [{ validator: validatePass, trigger: "change" }]
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          // eslint-disable-next-line
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }
};
</script>
<style lang="scss" scoped>
.login {
  height: 100%;
  min-height: 500px;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #3e3d3d;
  .login-wrap {
    width: 500px;
    height: 400px;
    background-color: #fff;
    border-radius: 4px;
    box-shadow: 2px 2px 15px #3d3d3d, -2px -2px 15px #3d3d3d;
    display: flex;
    align-items: center;
    justify-content: center;
    box-sizing: border-box;
    padding: 0 20px;
    .login-form {
      width: 100%;
    }

    // 登录按钮
    .login-submit {
      text-align: left;
      .login-submit-btn {
        width: 150px;
      }
    }
  }
}
</style>

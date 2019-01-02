<template>
  <div class="warp">
    <el-form label-position="top" label-width="80px" class="form" :model="formdata">
      <h3>用户登录</h3>
      <el-form-item label="用户名">
        <el-input v-model="formdata.username"></el-input>
      </el-form-item>
      <el-form-item label="密码">
        <el-input v-model="formdata.password"></el-input>
      </el-form-item>
      <el-button type="primary" class="btn" @click="handleLogin()">登录</el-button>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formdata: {
        username: "",
        password: ""
      }
    };
  },
  methods: {
    // 登录
    async handleLogin() {
      const res = await this.$http.post("login", this.formdata);
      console.log(res);

      const {
        data: {
          meta: { msg, status },
          data
        }
      } = res;
      if (status === 200) {
        localStorage.setItem("token", data.token);
        this.$router.push({
          name: "home"
        });
      } else {
        this.$message.warning(msg);
      }
    }
  }
};
</script>

<style>
.warp {
  height: 100%;
  background-color: #324152;
  display: flex;
  justify-content: center;
  align-items: center;
}
.form {
  background-color: white;
  border-radius: 10px;
  width: 400px;
  padding: 30px;
}
.btn {
  width: 100%;
}
</style>

<template>
<!--<HtmlLayout title="testTitle" description="vue server side render" keywords="egg, vue, webpack, server side render">-->
  <div id="all">
    <!--<h1>asdasd</h1>-->
    <div class="content">
      <el-row class="title" type="flex" justify="center">
        <el-col :span="12">
          蓝鸥IT考评系统
        </el-col>
      </el-row>
      <div class="bottom">
        <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px" :label-position='labelPosition'>
          <el-form-item label="电子邮箱" prop='u_email'>
            <el-input v-model="ruleForm.u_email" placeholder="请输入电子邮箱"></el-input>
          </el-form-item>
          <el-form-item label="密码" prop='u_pass'>
            <el-input v-model="ruleForm.u_pass" placeholder="请输入密码"></el-input>
          </el-form-item>
          <el-form-item label="验证码" prop='yzm'>
            <el-input v-model="ruleForm.yzm" placeholder="请输入验证码" style="width:60%"></el-input>
            <img src="../../asset/images/yzm.png" alt="yzm" style="height:40px;width:35%;">
          </el-form-item>
          <el-form-item>
            <el-button type="primary" @click="submitForm()" id="submit">立即登陆</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
<!--</HtmlLayout>-->
</template>

<script>
export default {
  data() {
    return {
      labelPosition: 'left',
      ruleForm: {
        u_email: '',
        u_password: '',
        yzm: ''
      },
      rules: {
        email: [
          { required: true, message: '请输入电子邮箱', trigger: 'blur' },
          { min: 1, max: 20, message: '长度不能超过 20 个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' }
        ],
        yzm: [
          { required: true, message: '请输入验证码', trigger: 'blur' }
        ]
      }
    };
  },
  methods: {
    submitForm() {
      console.dir(this.ruleForm);
      this.$http.post(this.domain + '/v1/sessions',this.ruleForm).then((res)=>{
        res = res.data;
        if(res.success === 1){
          window.location.href = '/public/afterlogin.html';
        }else{
          console.log('登录失败');
        }
      });

    }
  }
}
</script>


<style scoped>
#submit {
  width: 100%;
}
.el-form-item {
  margin-bottom: 40px;
}

#all {
  font-size: 16px;
  font-family: Microsoft YaHei;
  width: 100%;
  height: 99%;
  background-image: url("../../asset/images/login.jpg");
  background-position: center center;
  background-repeat: no-repeat;
  background-attachment: fixed;
  background-size: cover;
}

.content {
  width: 500px;
  min-width: 500px;
  margin: 0 auto;
  padding-top: 8%;
}

.title {
  color: #01AAED;
  font-family: Microsoft YaHei;
  font-size: 36px;
  width: 500px;
  min-width: 500px;
}

.bottom {
  margin-top: 50px;
  width: 500px;
  min-width: 500px;
}
</style>




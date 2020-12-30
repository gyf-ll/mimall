
<!--注册表单-->
<template>
  <div class="body">
    <img class="im" src="/static/img/login2.jpg" />
     <div class="logo">
     <img class="im2" src="/static/img/login.png" >
    </div>
    <div class="login-form">
      <i class="el-icon-user-solid"><span>华为账号注册</span></i><!--status-icon属性为输入框添加了校验结果的反馈图标-->
      <el-form ref="loginForm" :model="loginForm" :rules="loginFormru" label-width="80px" class="form" status-icon>
        <el-form-item label="用户账号" prop="name">
          <el-input placeholder="请输入账号" prefix-icon="el-icon-s-custom" v-model="loginForm.name" ></el-input>
        </el-form-item>
        <el-form-item label="账号密码" prop="password">
        <el-input placeholder="请输入密码" prefix-icon="el-icon-unlock" v-model="loginForm.password" show-password></el-input>
        </el-form-item>
        <el-form-item label="确认密码" prop="checkpas">
        <el-input prefix-icon="el-icon-unlock" v-model="loginForm.checkpas" autocomplete="off" show-password></el-input>
        </el-form-item>
        <el-form-item  class="btn">
        <el-button type="danger" plain  @click="zhuce">注册</el-button>
        <el-button  type="info" plain   @click="resetForm">重置</el-button>
        <p><router-link to="/login">已有账号,请登录>></router-link></p>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>

<script>
  export default {
     data() {
      var checkPass= (rule, value, callback) => {
        if (value === '') {
          callback(new Error('请再次输入密码'));
        } else if (value !== this.loginForm.password) {
          callback(new Error('两次输入密码不一致!'));
        } else {
          callback();
        }
      };
      return {
        loginForm: {
          name:'',
          password: '',
          checkpas: '',
          shopcar:[]
        },
        allRule: [],//空数组
        loginFormru: {
         name:[
           { required:true, message: '请输入账号名称', trigger: 'blur' },
          { min: 2, max: 10, message: '长度在2到10个字符', trigger: 'blur' }
        ],
        password:[
           { required:true, message: '密码不能为空', trigger: 'blur' },
          { min: 6, max: 10, message: '长度在6到10个字符', trigger: 'blur' }
        ],
         checkpas: [
                { validator:checkPass, trigger: 'blur' }
          ]
        },
      }
    },
    //获取信息
    created() {
      this.allRule = JSON.parse(localStorage.getItem('dataList'))
  },
  //添加信息
    methods: {
       zhuce() {
      this.$refs.loginForm.validate((valid)=>{
        if (valid) {
          if (localStorage.getItem('dataList')) {//当dataList表存在
            console.log(this.loginForm)
            this.allRule = JSON.parse(localStorage.getItem('dataList'))
            this.allRule.push(this.loginForm)//将allRule获取数据放进loginForm
            console.log(this.allRuleForm)//打印数据
            
            localStorage.setItem('dataList', JSON.stringify(this.allRule))//JSON.stringify()方法将JavaScript对象转换为字符串
          } 
          const valid = window.confirm('注册成功，跳到登录页面')
          if (valid) {
            this.$router.push('login' )//点击弹窗确定跳转到login页面
          }
        } else {
          alert('您还未完成注册');
          return false;
        }
      })//this调用函数，validate对整个表单进行校验的函数，参数为一个回调函数,=>箭头函数,valid形参,bloon值
    },
    //重置为初值，移除校验结果
     resetForm() {
        this.$refs.loginForm.resetFields();
      }
      }
    }
  
</script>


<style scoped>
.body {
  height: 650px;
  background-color: white;
}
.im {
  margin-left: -600px;
  margin-top: 120px;
  position: absolute;
}
.logo{
  margin-top:70px;
  margin-left:400px;
}
.im2{
  height:150px;
  width:200px;
  border:1px solid White;
  border-radius:50%;
}
.el-icon-user-solid {
  margin-top: 80px;
 
}
.login-form {
  height: 400px;
  width: 600px;
  margin: auto;
  margin-left: 650px;
  margin-top:-70px;
  background-color: rgba(247, 242, 242, 0.986);
}
.form{
  margin-top: 20px;
  margin-left: 150px;
  position:absolute;
}
.btn{
  display:flex;
 justify-content:right;
}
p:hover{
  color:lightsteelblue;
}
</style>

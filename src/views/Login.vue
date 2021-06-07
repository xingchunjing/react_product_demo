<template>
     <div class="login-container">
        <el-form :model="ruleForm" :rules="rules"
         status-icon
         ref="ruleForm" 
         label-position="left" 
         label-width="0px" 
         class="demo-ruleForm login-page">
            <h3 class="title">系统登录</h3>
            <el-form-item prop="name">
                <el-input type="text" 
                    v-model="ruleForm.name" 
                    auto-complete="off" 
                    placeholder="用户名"
                ></el-input>
            </el-form-item>
                <el-form-item prop="pass">
                    <el-input type="password" 
                        v-model="ruleForm.pass" 
                        auto-complete="off" 
                        placeholder="密码"
                    ></el-input>
                </el-form-item>
            <el-checkbox 
                v-model="checked"
                class="rememberme"
            >记住密码</el-checkbox>
            <el-form-item style="width:100%;">
                <el-button type="primary" style="width:100%;" @click="handleSubmit" :loading="logining">登录</el-button>
            </el-form-item>
        </el-form>
    </div>
</template>

<script>
    export default {
        name: 'login',
        data(){
            return{
                logining: false,
                ruleForm:{
                    name:'admin',
                    pass:'100uu100UU'
                },
                rules:{
                    name: [
                        {required:true,message:'请输入用户名',trigger: 'blur'},
                        {min:3,max:5,message:'长度在3-5个字符',trigger: 'blur'}
                    ],
                    pass: [
                        {required:true,message:'请输入密码',trigger: 'blur'},
                        {min:6,max:10,message:'长度在6-10个字符',trigger: 'blur'}
                    ],
                },
                checked: false
            }
        },
        methods: {

            handleSubmit(event){
                let {name,pass} = this.ruleForm
                this.$http({
                    method: 'post',
                    url: '/login',
                    data: {
                        name: name,
                        pass: pass
                    }
                }).then(res=>{
                    var code = res.data.code;
                    var msg = res.data.msg;
                    if(code=='200'){
                        console.log(code)
                        sessionStorage.setItem('name',name);
                        console.log(sessionStorage.getItem('name'))
                        
                        this.$router.push({name:'Home'})
                    }else{
                        alert(msg) 
                    }
                })
            }
        }
    }
</script>

<style scoped>
    .login-container {
        width: 100%;
        height: 100%;
    }
    .login-page {
        -webkit-border-radius: 5px;
        border-radius: 5px;
        margin: 180px auto;
        width: 350px;
        padding: 35px 35px 15px;
        background: #fff;
        border: 1px solid #eaeaea;
        box-shadow: 0 0 25px #cac6c6;
    }
    label.el-checkbox.rememberme {
        margin: 0px 0px 15px;
        text-align: left;
    }
</style>
<template>
    <div class="login"> 
        <p>登陆</p>
        <el-form :model="ruleForm" status-icon :rules="rules" ref="ruleForm" label-width="100px" class="demo-ruleForm">
            <el-form-item label="用户名" prop="name">
                <el-input v-model="ruleForm.name"></el-input>
            </el-form-item>
            <el-form-item label="密 码" prop="pass">
                <el-input type='password' v-model="ruleForm.pass"></el-input>
            </el-form-item>
            <el-form-item>
                <el-button type="primary" @click="login('ruleForm')">提交</el-button>
                <el-button @click="resetForm('ruleForm')">重置</el-button>
            </el-form-item>
            
        </el-form>
    </div>
</template>

<script>
    export default {
        name: 'login',
        data(){
            return{
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
                }
            }
        },
        methods: {
            login(formName) {
                let {name,pass} = this.ruleForm
                this.$http({
                    method: 'post',
                    url: '/login',
                    data: {
                        name: name,
                        pass: pass
                    }
                }).then(res=>{
                    console.log(res);
                    var code = res.data;
                    console.log(code)
                    if(code=='OK'){
                        console.log(code)
                        sessionStorage.setItem('name',name);
                        console.log(sessionStorage.getItem('name'))
                        
                        this.$router.push({name:'Home'})
                    }
                })
            },
            resetForm(formName) {
                this.$refs[formName].resetFields();
            }
        }
    }
</script>

<style>

</style>
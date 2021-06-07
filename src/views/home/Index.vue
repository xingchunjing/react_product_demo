<template>
  <el-container>
  <el-aside width="200px">Aside</el-aside>
  <el-container>
    <el-header>
      <el-button type="success" class="exit" @click="goBack()">退出</el-button>
      <div class="">
        <el-breadcrumb separator-class="el-icon-arrow-right">
        <el-breadcrumb-item :to="{ path: '/' }">首页</el-breadcrumb-item>
        <el-breadcrumb-item>活动管理</el-breadcrumb-item>
        <el-breadcrumb-item>活动列表</el-breadcrumb-item>
        <el-breadcrumb-item>活动详情</el-breadcrumb-item>
      </el-breadcrumb>
      </div>
    </el-header>
    <el-main>Main</el-main>
  </el-container>
</el-container>
</template>

<script>
export default {
  data(){
      return{

      }
  },
  methods: {
      goBack(){
          sessionStorage.removeItem("name");
          this.$router.push({name:'Login'})
      }
  }

}
</script>

<style>
  .el-header, .el-footer {
    background-color: #B3C0D1;
    color: #333;
    text-align: center;
    line-height: 60px;
  }
  
  .el-aside {
    background-color: #D3DCE6;
    color: #333;
    text-align: center;
    line-height: 200px;
  }
  
  .el-main {
    background-color: #E9EEF3;
    color: #333;
    text-align: center;
    line-height: 160px;
  }
  
  body > .el-container {
    margin-bottom: 40px;
  }
  
  .el-container:nth-child(5) .el-aside,
  .el-container:nth-child(6) .el-aside {
    line-height: 260px;
  }
  
  .el-container:nth-child(7) .el-aside {
    line-height: 320px;
  }
  .exit{
    float:right
  }
</style>
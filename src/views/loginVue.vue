<template>
  <div class="wrapper">
    <div
        style="margin: 200px auto; background-color: #fff; width: 350px; height: 300px; padding: 20px; border-radius: 10px">

      <div style="margin: 20px 0; text-align: center; font-size: 24px" ><b>登 录</b></div>


          <el-input size="medium" style="margin: 10px 0" prefix-icon="el-icon-user" v-model="adminname"></el-input>


          <el-input size="medium" style="margin: 10px 0" prefix-icon="el-icon-lock" show-password v-model="password"></el-input>

       <div>
          <el-button type="warning" size="small" autocomplete="off" >注册</el-button>
          <el-button type="primary" size="small" autocomplete="off" @click="login">登录</el-button>
    </div>

    </div>
  </div>
</template>

<script>
export default {
  name: "loginVue",
  data(){
    return{
      adminname: '',
      password:'',
      padding:''
    }
  },
  methods:{

    // login:function(){
    //   let _this=this;
    //
    //
    //   this.request.post('/login/',{
    //     adminname:this.adminname,
    //     password:this.password
    //   }).then(function (res) {
    //     console.log(res)
    //
    //
    //     alert('dengluchenggong');
    //
    //     _this.$router.push({path:'/'}
    //
    //     )
    //
    //   }).catch(function (e){
    //     alert('shibai')
    //     console.log(e)
    //   })
    //
    //
    // }
    login:function(){
      let _this=this;


      this.request.post('/login/',{
        adminname:this.adminname,
        password:this.password
      }).then(function (res) {
        console.log(res)

        if(res === 'dengluchenggong'){
          _this.$message.success('登陆成功')
          _this.$router.push({path:'/'})
        } else {
          _this.$message.error('登陆失败')
        }

      }).catch(function (e){
        console.log(e)
      })


    }


  }
}
</script>

<style>
.wrapper {
  height: 100vh;
  background-image: linear-gradient(to bottom right, #FC466B, #3F5EFB);
  overflow: hidden;
}
</style>
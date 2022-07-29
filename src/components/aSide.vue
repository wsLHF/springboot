<template>
  <el-menu :default-openeds="['1', '3']" style="min-height: 100%;overflow-x: hidden"
           background-color="rgb(48,65,86)"
           text-color="#fff"
           active-text-color="#ffd04b"
           :collapse-transition="false"
           :collapse="isCollpase"
           router
  >
    <div style="height: 60px;line-height: 60px;text-align: center">
      <img src="../assets/logo.png" alt="" style="width: 20px;position: relative;top:5px;margin-right: 5px">
      <b style="color: aliceblue" v-show="logoTextShow">后台管理系统</b>

    </div>



    <el-submenu index="1">
        <template slot="title">
          <i class="el-icon-house"></i>
          <span slot="title">用户信息修改</span>
        </template>
      <el-menu-item index="/admin">修改密码</el-menu-item>
    </el-submenu>

    <el-submenu index="2">
        <template slot="title">
        <i class="el-icon-menu"></i>
        <span slot="title">商品分类管理</span>
        </template>
          <el-menu-item-group>
                  <template slot="title">分类管理</template>
                  <el-menu-item index="/commodityClassify">分类维护</el-menu-item>
          </el-menu-item-group>
    </el-submenu>


    <el-submenu index="3">
      <template slot="title">
        <i class="el-icon-menu"></i>
        <span slot="title">商品管理</span>
      </template>
      <el-menu-item-group>
        <el-menu-item index="/commodity">商品维护</el-menu-item>
      </el-menu-item-group>


      <el-menu-item-group>
        <el-menu-item index="/purchase">进货</el-menu-item>
      </el-menu-item-group>

    </el-submenu>





    <el-submenu index="3">
      <template slot="title">
        <i class="el-icon-menu"></i>
        <span slot="title">商品展示</span>
      </template>
      <el-menu-item-group>
        <el-menu-item index="/display">查询商品</el-menu-item>
      </el-menu-item-group>
    </el-submenu>


    <el-submenu index="3">
      <template slot="title">
        <i class="el-icon-menu"></i>
        <span slot="title">出售管理</span>
      </template>
      <el-menu-item-group>
        <el-menu-item index="/sell">出售</el-menu-item>
      </el-menu-item-group>
    </el-submenu>







  </el-menu>
</template>

<script>
export default {
  name: "aSide",
  props:{
    isCollpase:Boolean,
    logoTextShow:Boolean
  }
}
</script>

<style scoped>

</style>
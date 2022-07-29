<template>


    <el-container style="min-height: 100vh; ">


      <el-aSide :width="sideWidth + 'px'" style="box-shadow: 2px 0 6px rgb(0 21 41 / 35%)">
        <aSide :isCollapse="isColpase" :logoTextShow="logoTextShow" style="padding-bottom: 20px"/>
      </el-aSide>

      <el-container>





        <el-main>
          <el-heaDer style="border-bottom: 1px solid #ccc;">

            <heaDer :collapseBtnClass="collapseBtnClass" :collapse="isColpase"/>

          </el-heaDer>


<!--          表示当前页面的子路由会在router-view里zhanshi-->
          <router-view />

        </el-main>
      </el-container>

    </el-container>

</template>

<script>
import aSide from "@/components/aSide";

import request from "@/utils/request";
import heaDer from "@/components/heaDer";

export default {
  name: 'HomeView',

  data(){

    return{
      tableData: [],
      total:0,
      pageNum:1,
      pageSize:2,
      username:"",
      dialogFormVisible:false,
      msg:"luoluo",
      form:{},
      isColpase:false,
      sideWideth:200,
      collapseBtnClass: 'el-icon-s-fold',
      sideWidth:200,
      logoTextShow:true

    }
  },

  components: {
    aSide,
    heaDer
  },
  methods:{
      collapse() {//点击收缩按钮收缩
        this.isColpase = !this.isColpase
        if (this.isColpase){//收缩
          this.sideWideth = 64
          this.collapseBtnClass='el-icon-s-unfold'
          this.logoTextShow = false

        }else {//展开

          this.sideWideth = 200
          this.collapseBtnClass = 'el-icon-s-fold'
          this.logoTextShow = true

        }

      },



  }
}
</script>

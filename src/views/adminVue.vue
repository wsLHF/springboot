<template>

  <div>


   <div style="width: 900px">


     <el-table :data="tableData" border stripe>
       <el-table-column prop="adminid" label="账户" ></el-table-column>
       <el-table-column prop="adminname" label="用户名" ></el-table-column>
       <el-table-column prop="password" label="密码" ></el-table-column>
       <el-table-column label="操作">
         <template slot-scope="scope">
           <!--              slot-scope="scope"-->
           <el-button type="success"  @click="handleEdit(scope.row)">编辑<i class="el-icon-edit"></i></el-button>

         </template>
       </el-table-column>
     </el-table>



     <el-dialog title="管理员信息" :visible.sync="dialogFormVisible" width="30%">
       <el-form label-width="80px" size="small">

         <el-form-item label="账户">
           <el-input v-model="form.adminid" autocomplete="off"></el-input>
         </el-form-item>

         <el-form-item label="用户名">
           <el-input v-model="form.adminname" autocomplete="off"></el-input>
         </el-form-item>

         <el-form-item label="密码">
           <el-input v-model="form.password" autocomplete="off"></el-input>
         </el-form-item>


       </el-form>
       <div slot="footer" class="dialog-footer">
         <el-button @click="dialogFormVisible = false">取 消</el-button>
         <el-button type="primary" @click="save">确 定</el-button>
       </div>
     </el-dialog>
   </div>



  </div>

</template>

<script>
import request from "@/utils/request";

export default {
  name: "修改密码",
  data(){
    return{
      tableData: [],
      total:0,
      pageNum:1,
      pageSize:2,
      adminname:"",
      dialogFormVisible:false,
      form:{},
      isColpase:false,
      sideWideth:200,
      collapseBtnClass: 'el-icon-s-fold',
      sideWidth:200,
      logoTextShow:true

    }


  },
  created() {
    this.load()
  }
  ,
  methods:{
    load(){
      request.get("/admin/adminpage",{
        params:{
          pageNum:this.pageNum,
          pageSize:this.pageSize,
          adminname:this.adminname
        }
      }).then(res => {
        console.log(res)
        this.tableData = res.data
        this.total = res.total
      })
      //请求分页查询数据
    },
    save(){
      this.request.post("/admin",this.form).then(res =>{
        if (res){
          this.$message.success("保存成功")
          this.dialogFormVisible = false
          this.load()
        } else {
          console.log(res)
          this.$message.error("保存失败")
        }
      })
    },
    handleAdd(){
      console.log()
      this.dialogFormVisible = true
      this.form = {}
    },
    handleEdit(row){
      this.form =row
      this.dialogFormVisible = true
    },
    del(adminid){
      request.delete("/admin/" + adminid).then(res =>{
        if (res){
          this.$message.success("删除成功")
          this.load()
        } else {
          this.$message.error("删除失败")
        }
      })
    },
    handleSizeChange(pageSize){
      console.log(pageSize)
      this.pageSize=pageSize
      this.load()
    },
    handleCurrentChange(pageNum){
      console.log(pageNum)
      this.pageNum=pageNum
      this.load()
    }
  }
}








</script>

<style scoped>

</style>
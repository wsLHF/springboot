<template>
<div >
  <div style="margin: 10px 0">
    <el-button type="primary" @click="handleAdd">新增<i class="el-icon-circle-plus-outline"></i></el-button>

    <el-button type="primary">导入<i class="el-icon-bottom"></i></el-button>
    <el-button type="primary">导出<i class="el-icon-top"></i></el-button>
  </div>

  <el-table :data="tableData" border stripe>
    <el-table-column prop="classifyid" label="商品分类ID" width="330"></el-table-column>
    <el-table-column prop="classifyname" label="商品分类" width="330"></el-table-column>

    <el-table-column label="操作">
      <template slot-scope="scope">
        <!--              slot-scope="scope"-->
        <el-button type="success"  @click="handleEdit(scope.row)">编辑<i class="el-icon-edit"></i></el-button>
        <el-popconfirm
            class="ml-5"
            confirm-button-text='确定'
            cancel-button-text='我再想想'
            icon="el-icon-info"
            icon-color="red"
            title="确定删除吗？"
            @confirm="del(scope.row.classifyid)"
        >
          <el-button type="danger" slot="reference">删除<i class="el-icon-remove-outline"></i></el-button>
        </el-popconfirm>
      </template>
    </el-table-column>
  </el-table>


  <div style="padding: 10px 0">
    <el-pagination
        @size-change="handleSizeChange"
        @current-change="handleCurrentChange"

        :current-page="pageNum"
        :page-sizes="[3, 5, 10, 20]"
        :page-size="pageSize"
        layout="total, sizes, prev, pager, next, jumper"
        :total="total">
    </el-pagination>

  </div>



  <el-dialog title="商品信息" :visible.sync="dialogFormVisible" width="30%">
        <el-form label-width="80px" size="small">
<!--           <el-form-item label="商品ID">-->
<!--                   <el-input v-model="form.classifyid" autocomplete="off"></el-input>-->
<!--          </el-form-item>-->
          <el-form-item label="商品分类">
                 <el-input v-model="form.classifyname" autocomplete="off"></el-input>
          </el-form-item>
        </el-form>
    <div slot="footer" class="dialog-footer">
      <el-button @click="dialogFormVisible = false">取 消</el-button>
      <el-button type="primary" @click="save">确 定</el-button>
    </div>
  </el-dialog>





</div>




</template>

<script>
import request from "@/utils/request";

export default {
  name: "分类维护",
  data(){
    return{
      tableData: [],
      total:0,
      pageNum:1,
      pageSize:3,
      classifyname:"",
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
      request.get("/classify/classifypage",{
        params:{
          pageNum:this.pageNum,
          pageSize:this.pageSize,
          classifyname:this.classifyname
        }
      }).then(res => {
        console.log(res)
        this.tableData = res.data
        this.total = res.total
      })
      //请求分页查询数据
    },
    save(){
      this.request.post("/classify",this.form).then(res =>{
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
    del(classifyid){
      request.delete("/classify/" + classifyid).then(res =>{
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
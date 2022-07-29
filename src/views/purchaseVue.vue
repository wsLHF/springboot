<template>
<div>
  <div>
    <div style="margin: 10px 0">
<!--      <el-input style="width: 200px" placeholder="请输入名称" suffix-icon="el-icon-search" v-model="commodityname"></el-input >-->
<!--      <el-input style="width: 200px" placeholder="请输入批次" suffix-icon="el-icon-message" v-model="batch"></el-input >-->
<!--      <el-input style="width: 200px" placeholder="请输入保质期" suffix-icon="el-icon-position" v-model="qualitydate"></el-input >-->
<!--      <el-button class="ml-5" type="primary" @click="load">选择</el-button>-->
    </div>
    <div style="margin: 10px 0">
      <el-button type="primary" @click="handleAdd">进货<i class="el-icon-circle-plus-outline"></i></el-button>
<!--      <el-button type="danger">批量删除<i class="el-icon-remove-outline"></i></el-button>-->
<!--      <el-button type="primary">导入<i class="el-icon-bottom"></i></el-button>-->
<!--      <el-button type="primary">导出<i class="el-icon-top"></i></el-button>-->

    </div>
    <el-table :data="tableData" border stripe>
      <el-table-column prop="commodityid" label="商品ID" width="80"></el-table-column>
      <el-table-column prop="commodityclassify" label="商品分类" width="80"></el-table-column>
      <el-table-column prop="commodityname" label="商品名称" width="80"></el-table-column>
      <el-table-column prop="batch" label="进货批次"></el-table-column>
      <el-table-column prop="productiondate" label="生产日期"></el-table-column>
      <el-table-column prop="qualitydate" label="保质期"></el-table-column>
      <el-table-column prop="price1" label="进货价格"></el-table-column>
      <el-table-column prop="price2" label="标准价"></el-table-column>
      <el-table-column prop="exist" label="库存"></el-table-column>
<!--      <el-table-column label="操作">-->
<!--        <template slot-scope="scope">-->
<!--          &lt;!&ndash;              slot-scope="scope"&ndash;&gt;-->
<!--          <el-button type="success"  @click="handleEdit(scope.row)">编辑<i class="el-icon-edit"></i></el-button>-->
<!--          <el-popconfirm-->
<!--              class="ml-5"-->
<!--              confirm-button-text='确定'-->
<!--              cancel-button-text='我再想想'-->
<!--              icon="el-icon-info"-->
<!--              icon-color="red"-->
<!--              title="确定删除吗？"-->
<!--              @confirm="del(scope.row.commodityid)"-->
<!--          >-->
<!--            <el-button type="danger" slot="reference">删除<i class="el-icon-remove-outline"></i></el-button>-->
<!--          </el-popconfirm>-->
<!--        </template>-->
<!--      </el-table-column>-->
    </el-table>

    <div style="padding: 10px 0">
      <el-pagination
          @size-change="handleSizeChange"
          @current-change="handleCurrentChange"

          :current-page="pageNum"
          :page-sizes="[2, 10, 15, 20]"
          :page-size="pageSize"
          layout="total, sizes, prev, pager, next, jumper"
          :total="total">
      </el-pagination>

    </div>

    <el-dialog title="商品信息" :visible.sync="dialogFormVisible" width="30%">
      <el-form label-width="80px" size="small">

        <el-form-item label="商品ID">
          <el-input v-model="form.commodityid" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="商品分类">
          <el-input v-model="form.commodityclassify" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="商品名称">
          <el-input v-model="form.commodityname" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="进货批次">
          <el-input v-model="form.batch" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="生产日期">
          <el-input v-model="form.productiondate" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="保质期">
          <el-input v-model="form.qualitydate" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="进价">
          <el-input v-model="form.price1" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="标准售价">
          <el-input v-model="form.price2" autocomplete="off"></el-input>
        </el-form-item>

        <el-form-item label="库存">
          <el-input v-model="form.exist" autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="商品图片" prop="image">
          <el-button type="primary" @click="innerVisibleImg = true">上传图片</el-button>
        </el-form-item>

      </el-form>
      <div slot="footer" class="dialog-footer">
        <el-button @click="dialogFormVisible = false">取 消</el-button>
        <el-button type="primary" @click="save">确 定</el-button>
      </div>

      <el-dialog
      width="40%"
      title="上传图片"
      :visible.sync="innerVisibleImg"
      append-to-body
      >
        <UploadImg/>
        <span slot="footer" class="=dialog-footer">
          <el-button @click="innerVisibleImg = false">取消</el-button>
          <el-button type="primary" @click="innerVisibleImg = false">确定</el-button>
        </span>


      </el-dialog>

    </el-dialog>
  </div>
</div>
</template>

<script>
import UploadImg from "@/components/UploadImg"
export default {
  name: "进货",
  components:{
    UploadImg
  },
  data(){
    return{
      dialogVisible:false,
      innerVisible:false,
      innerVisibleImg:false,

      tableData: [],
      total:0,
      pageNum:1,
      pageSize:5,
      commodityname:"",
      batch:"",
      qualitydate:"",
      dialogFormVisible:false,
      msg:"luoluo",
      form:{},
      isColpase:false,
      sideWideth:200,
      collapseBtnClass: 'el-icon-s-fold',
      sideWidth:200,
      logoTextShow:true
    }
  },created() {
    this.load()
  },
  methods:{
    load(){
      this.request.get("/commodity/commoditypage",{
        params:{
          pageNum:this.pageNum,
          pageSize:this.pageSize,
          commodityname:this.commodityname,
          batch:this.batch,
          // qualitydate:this.qualitydate,
        }
      }).then(res => {
        console.log(res)
        this.tableData = res.data
        this.total = res.total
      })
      //请求分页查询数据
    },
    save(){
      this.request.post("/commodity",this.form).then(res =>{
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
    del(commodityid){
      this.request.delete("/commodity/" + commodityid).then(res =>{
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
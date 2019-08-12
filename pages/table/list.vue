<template>
  <div class="list">
    <el-table
    :data="tableData"
    border
    style="width: 100%">
    <el-table-column
      fixed
      prop="date"
      label="日期"
     >
    </el-table-column>
     <el-table-column
      prop="title"
      label="标题"
      >
    </el-table-column>
    <el-table-column
      prop="done"
      label="已完成"
      >
    </el-table-column>
    <el-table-column
      prop="doing"
      label="进行中"
      >
    </el-table-column>
    <el-table-column
      prop="toDo"
      label="未完成"
      >
    </el-table-column>
   

    <el-table-column
      fixed="right"
      label="操作"
      >
      <template slot-scope="scope">
        <el-button type="text" size="small" @click.native="edit(scope.row,1)">编辑</el-button>
        <el-button type="text" size="small" @click.native="del(scope.row)">删除</el-button>
      </template>
    </el-table-column>
  </el-table>

  <div>
    <div>
       <el-dialog title="新增数据" :visible.sync="dialogFormVisible" width="40%">
        <el-form :model="detailObj">
          <el-form-item label="时间" :label-width="formLabelWidth">
            <el-date-picker
            style="margin:0;width:100%;"
              v-model="detailObj.date"
              type="date"
              format="yyyy-MM-dd"
              placeholder="选择日期">
            </el-date-picker>
          </el-form-item>
          <el-form-item label="标题" :label-width="formLabelWidth">
            <el-input v-model="detailObj.title" autocomplete="off"></el-input>
          </el-form-item>
     
               <el-form-item label="已完成"  :label-width="formLabelWidth">
            <el-input v-model="detailObj.done" type="textarea" autocomplete="off"></el-input>
          </el-form-item>
        
           <el-form-item label="进行中" :label-width="formLabelWidth">
            <el-input v-model="detailObj.doing" type="textarea" autocomplete="off"></el-input>
          </el-form-item>
             <el-form-item label="未完成" :label-width="formLabelWidth">
            <el-input v-model="detailObj.toDo" type="textarea" autocomplete="off"></el-input>
          </el-form-item>
        </el-form>
    
        <div slot="footer" class="dialog-footer">
          <el-button @click="dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="sure">确 定</el-button>
        </div>
      </el-dialog>
    </div>
  </div>
  </div>

</template>

<script>
import Detail from './detail.vue'

  export default {
    props:['tableData'],
    components: {
      Detail,
    },

    data() {
      return {
        detailObj:{},
        dialogFormVisible:false,
        dialogVisible: false,
        formLabelWidth:'120px'
 
      }
    },
     methods: {
    
      del(index) {
        this.tableData.splice(index,1)
         localStorage.setItem('tableData',JSON.stringify(this.tableData))
      },
      edit(val,index) {
        if(index && index === 1) {
          this.dialogFormVisible = true;

          this.detailObj = val
        }

      },
      sure() {
          this.dialogFormVisible = false;

        localStorage.setItem('tableData',JSON.stringify(this.tableData))

      }
    },
  }
</script>
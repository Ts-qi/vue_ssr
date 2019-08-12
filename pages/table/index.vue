<template>
  <div class="table-list">
    <div class="tools">
      <div class=" add">
        <el-button type="primary" size="mini"  @click="add(2)" >新增数据</el-button>

      </div>
      <div class="search">
        <el-input 
          size="mini"
          v-model="searchName" 
          @keyup.enter.native="search"
          placeholder="请输入内容"
          ></el-input>
      </div>
    </div>
    <div class="list">
      <List 
        :tableData="tableData">
        </List>
    </div>

    <div>
       <el-dialog title="新增数据" :visible.sync="dialogFormVisible" width="40%">
        <el-form :model="form">
          <el-form-item label="时间" :label-width="formLabelWidth">
            <el-date-picker
            style="margin:0;width:100%;"
              v-model="form.date"
              type="date"
              format="yyyy-MM-dd"
              placeholder="选择日期">
            </el-date-picker>
          </el-form-item>
          <el-form-item label="标题" :label-width="formLabelWidth">
            <el-input v-model="form.title" autocomplete="off"></el-input>
          </el-form-item>
     
               <el-form-item label="已完成"  :label-width="formLabelWidth">
            <el-input v-model="form.done" type="textarea" autocomplete="off"></el-input>
          </el-form-item>
        
           <el-form-item label="进行中" :label-width="formLabelWidth">
            <el-input v-model="form.doing" type="textarea" autocomplete="off"></el-input>
          </el-form-item>
             <el-form-item label="未完成" :label-width="formLabelWidth">
            <el-input v-model="form.toDo" type="textarea" autocomplete="off"></el-input>
          </el-form-item>
        </el-form>
    
        <div slot="footer" class="dialog-footer">
          <el-button @click="dialogFormVisible = false">取 消</el-button>
          <el-button type="primary" @click="sure">确 定</el-button>
        </div>
      </el-dialog>
    </div>

    
  </div>
</template>
<script>
import List from './list.vue'
export default{
  components: {
  List,
  },
  data() {
    return {
      searchName:'',
      value1:'',
      tableData: [],
      dialogFormVisible: false,
      form: {
        title: '',
        toDo: '',
        date: '',
        doing: '',
        done: '',
      },
      formLabelWidth: '120px'
    }
  },
  created() {

  },
  mounted() {
    if(localStorage) {
    let data = JSON.parse(localStorage.tableData)
    this.tableData = data;
    console.log(data,'data')
    }
  },
  methods:{
    search() {
     let  arrs=[]
      if( this.searchName !='') {
         arrs =  this.tableData.filter(ele => ele.title == this.searchName);
      console.log( this.tableData,'v1')

      }else{
        let data = JSON.parse(localStorage.tableData)
        arrs = data;

      }

      this.tableData = arrs
    },
  timeCHange(time){
    var d = new Date(time); 
    var datetime=d.getFullYear() + '-' + (d.getMonth() + 1) + '-' + d.getDate();
    return datetime
  },
  add(index) {
    if(index === 2) {

      this.dialogFormVisible = true
      this.form = {
        title: '',
        toDo: '',
        date: '',
        doing: '',
        done: '',
      }
    }
    localStorage.setItem('tableData',JSON.stringify(this.tableData))

  },
  sure() {
      let {title, toDo, date,doing,done} = this.form;
      let time = this.timeCHange(date)
      console.log(this.form)
      this.tableData.unshift({
        title: title,
        toDo: toDo,
        date: time,
        doing: doing,
        done: done,
      })
    localStorage.setItem('tableData',JSON.stringify(this.tableData))

      this.dialogFormVisible = false
    }
  }
}
</script>
<style  scope>
  .table-list {
    text-align: center;
    margin: 20px auto;
  }
  .tools {
    display: flex;
    border: 1px solid #eeeeee;
    padding:10px;
  }

  .add {
    flex: 1;
    text-align: left;
  }
   .search {
    flex: 1;
    text-align: right;
  }
  .search input {
    width: 60%;
  }
  .list{
    margin-top: 20px;
  }

</style>
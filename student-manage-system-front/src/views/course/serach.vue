<template>
  <div>
    <el-input placeholder="请输入内容" v-model="content" class="input-with-select"
              style="margin-top: 15px;width:50%;margin-left: 15px;">
      <el-select v-model="select" slot="prepend" placeholder="请选择">
        <el-option label="工号" value="1"></el-option>
        <el-option label="姓名" value="2"></el-option>
      </el-select>
      <el-button slot="append" icon="el-icon-search" @click="handleSearch()"></el-button>
    </el-input>

    <el-table
      :data="tableData"
      border
      style="margin-top: 15px;width:90%;margin-left: 15px;">
      <el-table-column
        label="序号"
        width=""
        align="center">
        <template slot-scope="scope">
          {{ scope.row.id }}
        </template>
      </el-table-column>
      <el-table-column
        label="课程名称"
        width=""
        align="center">
        <template slot-scope="scope">
          {{ scope.row.name }}
          </el-popover>
        </template>
      </el-table-column>
      <el-table-column
        label="授课教师"
        width=""
        align="center">
        <template slot-scope="scope">
          {{ scope.row.teacher }}
          </el-popover>
        </template>
      </el-table-column>
      <el-table-column
        label="教室位置"
        width=""
        align="center">
        <template slot-scope="scope">
          {{ scope.row.date }}
          </el-popover>
        </template>
      </el-table-column>
      <el-table-column
        label="上课时间"
        width=""
        align="center">
        <template slot-scope="scope">
          {{ scope.row.time }}
          </el-popover>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<style>
  .el-select .el-input {
    width: 130px;
  }
  .input-with-select .el-input-group__prepend {
    background-color: #fff;
  }
</style>
<script type="text/javascript">
  import {searchCourse} from '@/api/course'
  export default {
    data() {
      return {
        tableData: [],
        content: '',
        select: ''
      }
    },
    methods: {
      handleSearch(){
        var content = this.content;
        var select = this.select;
        var data = {
          content: content,
          select: select
        }
        if(select == null || "" == select){
          this.$message({
            message: "选择查询类别",
            type: 'error'
          });
          return;
        }

        if(content == null || "" == content){
          this.$message({
            message: "查询内容不能为空",
            type: 'error'
          });
          return;
        }
        searchCourse(data).then(
          response=>{
            this.tableData = [];
            if(response.data.length == 0){
              this.$message({
                message: "无匹配结果",
                type: 'warning'
              });
            }else{
              this.tableData = response.data;
            }

          }
        )
      }
    }
  }
</script>

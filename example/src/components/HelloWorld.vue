<template>
  <div>
    <el-button type="primary" @click="add">HelloWorld组件</el-button>
    <el-table :data="tableData" style="width: 100%">
      <el-table-column prop="date" label="日期" width="180"></el-table-column>
      <el-table-column prop="name" label="姓名" width="180"></el-table-column>
      <el-table-column prop="address" label="地址"></el-table-column>
      <el-table-column label="操作">

        <!--
          这里拿到每一行的index----------scope.$index
          这里拿到每一行的数据-----------scope.$row
          scope.index在触发的函数中，传递参数，methods里面的函数handleClick（index,row）{}直接用就可以了
         -->
        <template slot-scope="scope">
          <el-button size="mini" type="danger" @click="handleDelete(scope.$index, scope.row)">删除</el-button>
        </template>
      </el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tableData: [
        {
          date: "2016-05-02",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1518 弄"
        },
        {
          date: "2016-05-04",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1517 弄"
        },
        {
          date: "2016-05-01",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1519 弄"
        }
      ]
    };
  },
  methods: {
    add() {
      this.tableData.push({
        date: "2016-05-01",
        name: "王小虎",
        address: "上海市普陀区金沙江路 1519 弄"
      });
    },
    handleDelete(index,row){
      this.tableData.splice(index,1);
    },
  }
};
</script>

<style lang="scss" scoped>
</style>
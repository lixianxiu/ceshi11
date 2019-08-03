<template>
  <el-table :data="tableData">
    <el-table-column v-for="(col) in clolumns" :key="col.prop" v-bind="col"></el-table-column>
  </el-table>
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
        },
        {
          date: "2016-05-03",
          name: "王小虎",
          address: "上海市普陀区金沙江路 1516 弄"
        }
      ],
      clolumns: [
        {
          prop: "date",
          lable: "one"
        },
        {
          prop: "name",
          lable: "one"
        },
        {
          prop: "adress",
          lable: "one"
        },
        {
          prop: "select",
          lable: "operate",

          formatter: (row, cloumcell, index) => {
            return <el-button>add it</el-button>;
          }
        }
      ]
    };
  }
};
</script>

<style>
</style>

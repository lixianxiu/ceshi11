<template>
  <div>
    <el-table :data="tableData" border sytle="width:400px" @cell-dblclick="handleChange">
      <el-table-column v-for="(col) in clolumns" :key="col.prop" v-bind="col"></el-table-column>
    </el-table>
    <h1>实现一个可以添加的表格</h1>
    <h2>the think is :</h2>
  </div>
</template>

<script>
export default {
  props: {
    edit: {
      type: Boolean,
      default: true
    }
  },
  created() {
    this.edit && this.init();
  },
  data() {
    return {
      tableData: [
        {
          date: "",
          name: "",
          address: ""
          // edit: false
        }
      ],
      clolumns: [
        {
          prop: "date",
          label: "one",
          formatter: (row, cloumcell, index) => {
            console.log(row.edit);
            if (row.edit) {
              return (
                <el-input value={row.date} onInput={e => (row.date = e)}>
                  add it
                </el-input>
              );
            } else {
              return <span></span>;
            }
          }
        },
        {
          prop: "name",
          label: "one",
          formatter: (row, cloumcell, index) => {
            if (row.edit) {
              return (
                <el-input value={row.name} onInput={e => (row.name = e)}>
                  add it
                </el-input>
              );
            } else {
              return <span></span>;
            }
          }
        },
        {
          prop: "address",
          label: "one",
          formatter: (row, cloumcell, index) => {
            if (row.edit) {
              return (
                <el-input value={row.address} onInput={e => (row.address = e)}>
                  add it
                </el-input>
              );
            } else {
              return <span>{row.address}</span>;
            }
          }
        },
        {
          prop: "select",
          label: "operate",
          formatter: (row, cloumcell, index) => {
            return (
              <el-button onClick={val => this.addList()}>add it</el-button>
            );
          }
        }
      ]
    };
  },

  methods: {
    //edit init option assign
    init() {
      this.tableData.map(list => {
        this.$set(list, "edit", false);
      });
    },
    addList(row, cell, index) {
      debugger
    },
    handleChange(row, column, cell, event) {
      console.log(row);
      row.edit = !row.edit;
    }
  }
};
</script>

<style>
</style>

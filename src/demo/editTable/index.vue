<template>
  <div>
    <el-table :data="tableData" border>
      <el-table-column width="200px" v-for="col in columns " :key="col.prop" v-bind="col"></el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: "editTable",
  data() {
    return {
      tableData: [
        {
          date: "",
          name: "",
          address: " ",
          optionExample: "",
          isRequired: "",
          desc: " "
        },
        {
          date: "",
          name: "",
          address: " ",
          optionExample: "",
          isRequired: "",
          desc: " "
        },
        {
          date: "",
          name: "",
          address: " ",
          optionExample: "",
          isRequired: "",
          desc: " "
        },
        {
          date: "",
          name: "",
          address: " ",
          optionExample: "",
          isRequired: "",
          desc: " "
        }
      ],
      columns: [
        {
          label: "参数名",
          prop: "name",
          formatter: (row, cell, index) => {
            // console.log(row, cell);
            return (
              <el-input
                value={row.name}
                onInput={val => {
                  this.handleName(val, row);
                }}
              ></el-input>
            );
          }
        },
        {
          label: "参数type",
          prop: "date",
          formatter: (row, cell, index) => {
            return (
              <el-input
                value={row.date}
                onInput={val => {
                  this.handleData(val, row);
                }}
              ></el-input>
            );
          }
        },
        {
          label: "isRuquired",
          prop: "isRequired",
          formatter: (row, cell, index) => {
            return (
              <el-input
                value={row.isRequired}
                onInput={val => {
                  this.handleisRequired(val, row);
                }}
              ></el-input>
            );
          }
        },
        {
          label: "desc",
          prop: "desc",
          formatter: (row, cell, index) => {
            return (
              <el-input
                value={row.desc}
                onInput={val => {
                  this.handleDesc(val, row);
                }}
              ></el-input>
            );
          }
        },
        {
          label: "optionExample",
          prop: "optionExample",
          formatter: (row, cell, index) => {
            return (
              <el-input
                value={row.optionExample}
                onInput={val => {
                  this.handleoptionExample(val, row);
                }}
              ></el-input>
            );
          }
        },
        {
          label: "operate",
          //   prop: "",
          formatter: (row, cell, index) => {
            return (
              <div>
                <el-button>delete</el-button>
                <el-button>save</el-button>
              </div>
            );
          }
        }
      ]
    };
  },
  methods: {
    handleName(e, row) {
      row.name = e;
    },
    handleData(e, row) {
      //   debugger;
      row.date = e;
    },
    handleDesc(e, row) {
      row.desc = e;
    },
    handleisRequired(e, row) {
      row.isRequired = e;
    },
    handleoptionExample(e, row) {
      row.optionExample = e;
    }
  }
};
</script>

<style>
</style>

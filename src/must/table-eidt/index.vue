<template>
  <div>
    <el-table :data="data" border sytle="width:400px" @cell-dblclick="handleChange">
      <el-table-column v-for="(col) in clolumns" :key="col.prop" v-bind="col"></el-table-column>
    </el-table>
    <h1>实现一个可以添加编辑的表格</h1>
    <h2>the think is : who's data who handlewith</h2>
  </div>
</template>

<script>
export default {
  props: {
    edit: {
      type: Boolean,
      default: false
    },
    data: {
      type: Array,
      default: () => {
        return [
          {
            date: "",
            name: "",
            address: ""
            // edit: false
          }
        ];
      }
    }
  },
  created() {
    console.log(this.data);
    this.edit && this.init();
  },
  data() {
    return {
      clolumns: [
        {
          prop: "date",
          label: "your date",
          formatter: (row, cloumcell, index) => {
            console.log(row.edit);
            if (row.edit) {
              return (
                <el-input value={row.date} onInput={e => (row.date = e)}>
                  add it
                </el-input>
              );
            } else {
              return <span>{row.date}</span>;
            }
          }
        },
        {
          prop: "name",
          label: " your name",
          formatter: (row, cloumcell, index) => {
            if (row.edit) {
              return (
                <el-input
                  placeholder="edit name"
                  value={row.name}
                  onInput={e => (row.name = e)}
                >
                  add it
                </el-input>
              );
            } else {
              return <span>{row.name}</span>;
            }
          }
        },
        {
          prop: "address",
          label: "your address",
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
          formatter: (row, cloumcell, index, evevt) => {
            if (evevt !== 0) {
              return (
                <div>
                  <el-button onClick={val => this.addList}>add_it</el-button>
                  <el-button onClick={val => this.deleteoneList(evevt)}>
                    delet_it
                  </el-button>
                </div>
              );
            } else {
              return (
                <el-button onClick={val => this.addList}>add_it</el-button>
              );
            }
          }
        }
      ]
    };
  },

  methods: {
    init() {
      this.data.map(list => {
        this.$set(list, "edit", false);
      });
    },
    addList() {
      this.$emit("addObject");
      this.init();
    },
    deleteoneList(idx) {
      this.$emit("deletOneObject", idx);
    },
    handleChange(row, column, cell, event) {
      row.edit = !row.edit;
    }
  }
};
</script>

<style>
</style>

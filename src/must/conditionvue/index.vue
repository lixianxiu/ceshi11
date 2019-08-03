<template>
  <div>
    <el-table :data="tableData">
      <el-table-column v-for="col in columns" :key="col.prop" v-bind="col"></el-table-column>
    </el-table>
  </div>
</template>

<script>
export default {
  name: "conditionSelect",
  data() {
    return {
      radioValue: "",
      radioValue2: "1",
      checkValue: [],
      checkValue2: [],
      value: "",
      tableData: [
        {
          interfaceId: 1,
          desc: "2016-05-02",
          ra1: false,
          required: "0",
          englishName: "a_b_c_d_ddd",
          chinaName: "上海市普陀区金沙江路 1518 弄"
        },
        {
          interfaceId: 2,
          desc: "2016-05-04",
          ra1: false,
          required: "0",
          englishName: "a_b_c_d_ddd",
          chinaName: "上海市普陀区金沙江路 1517 弄"
        },
        {
          interfaceId: 3,
          desc: "2016-05-01",
          ra1: false,
          required: "0",
          englishName: "a_b_c_d_ddd",
          chinaName: "上海市普陀区金沙江路 1519 弄"
        },
        {
          interfaceId: 4,
          desc: "2016-05-03",
          ra1: false,
          required: "0",
          englishName: "a_b_c_d_ddd",
          chinaName: "上海市普陀区金沙江路 1516 弄"
        }
      ],
      columns: [
        {
          label: "表英文名",
          prop: "englishName"
        },
        {
          label: "表中文名",
          prop: "chinaName"
        },
        {
          label: "元数据描述",
          prop: "desc"
        },
        {
          label: "条件",
          prop: "select_raido",
          formatter: (row, column, valuCell, index) => {
            return (
              <el-checkbox
                value={this.checkValue}
                label={row.interfaceId}
                onChange={val => this.checkChange(val, row.interfaceId, row)}
              >
                &nbsp;
              </el-checkbox>
            );
          }
        },
        {
          label: "默认不能选",
          prop: "select_no_select",
          formatter: (row, column, index) => {
            return (
              <el-checkbox
                disabled={!row.ra1}
                value={this.checkValue2}
                label={row.interfaceId}
                onChange={val => this.checkChange1(val, row.interfaceId, row)}
              >
                &nbsp;
              </el-checkbox>
            );
          }
        }
      ]
    };
  },
  methods: {
    checkedChange(val, id, row, arr) {
      const curIndex = arr.findIndex(item => item === id);
      const has = !!val && curIndex === -1;
      if (has) {
        arr.push(id);
      } else {
        arr.splice(curIndex, 1);
      }
    },
    checkChange(val, id, row) {
      //if find it ,return INdex or -1;
      this.checkedChange(val, id, row, this.checkValue);
      row.ra1 = !row.ra1;
      if (!val) {
        const hasIndex = this.checkValue2.findIndex(item => item === id);
        this.checkValue2.splice(hasIndex, 1);
      }
    },
    //操作传进来的对象让其erquired为1;
    checkChange1(val, id, row) {
      this.checkedChange(val, id, row, this.checkValue2);
      row.required = row.required === "0" ? "1" : "0";
      console.log(row);
    }
  }
};
</script>

<style>
</style>

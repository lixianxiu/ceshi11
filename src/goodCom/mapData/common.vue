<template>
  <div>
    <el-container>
      <el-header>
        <el-row :gutter="20">
          <el-col :span="5">
            <el-select v-model="value" placeholder="请选择">
              <el-option
                v-for="item in options"
                :key="item.value"
                :label="item.label"
                :value="item.value"
              ></el-option>
            </el-select>
          </el-col>
          <el-col :span="5">
            <el-input></el-input>
          </el-col>
          <el-col :span="5">
            <el-button>search</el-button>
          </el-col>
          <el-col :span="3">
            <slot>
              <el-button>preserve</el-button>
            </slot>
          </el-col>
        </el-row>
      </el-header>
      <el-main>
        <el-table :data="data" style="width: 100%" border>
          <!-- <el-table-column label="" width="50" type="index"></el-table-column>
          <el-table-column prop="date" label="日期" width="180"></el-table-column>
          <el-table-column prop="name" label="姓名" width="180"></el-table-column>
          <el-table-column prop="address" label="地址"></el-table-column>
          <el-table-column label="change" width="80">
            <template scope="scope">
              <el-radio
                v-if="type==='radio'"
                v-model="radio"
                :label="scope.$index"
                @change.native="getTemplateRow(scope.$index,scope.row)"
              >&nbsp;</el-radio>
              <el-checkbox
                v-if="type==='checked'"
                v-model="checkout"
                :label="scope.$index"
                @change.native="handleEdit(scope.$index,scope.row)"
              >&nbsp;</el-checkbox>
            </template>
          </el-table-column>-->
          <el-table-column v-for="(col) in columns" :key="col.prop" v-bind="col"></el-table-column>
        </el-table>
      </el-main>
    </el-container>
  </div>
</template>

<script>
import { constants } from "crypto";
export default {
  name: "dataMap",
  props: {
    data: Array,
    type: String
  },
  data() {
    return {
      checkout: [],
      columns: [
        {
          prop: "date",
          label: "日期"
        },
        {
          prop: "name",
          label: "姓名"
        },
        {
          prop: "address",
          label: "地址"
        },
        {
          prop: "select_raido",
          label: "选取",
          formatter: (row, column, celslValue, index) => {
            console.log(row);
            console.log(index, "index");
            // return <el-radio value={this.radioValue} label={index} onChange={val=>this.radioChange(index)}>&nbsp;</el-radio>
            return (
              <el-checkbox
                value={this.selectData}
                onChange={val => this.checkChange(val, row.id,row)}
                // checked = {index}
              ></el-checkbox>
            );
          }
        }
      ],
      radio: "",
      options: [
        {
          value: "选项1",
          label: "黄金糕"
        },
        {
          value: "选项2",
          label: "双皮奶"
        }
      ],
      value: "",
      radioValue: 1,
      selectData: []
    };
  },
  methods: {
    getTemplateRow(index, row) {
      console.log(index, row);
      this.radio = index;
      console.log(this.radio);
    },
    handleEdit(index, row) {
      console.log(index, row);
      console.log(this.checkout);
    },
    radioChange(val) {
      console.log(val);
      // debugger
      this.radioValue = val;
    },
    checkChange(val, id,row) {
      debugger
      const curIndex = this.selectData.findIndex(item => item === id);
      Number(curIndex + 1);
      const isExist = !!val && curIndex === -1;

      console.log(isExist);
      if (isExist) {
        this.selectData.push(id);
      } else {
        this.selectData.splice(curIndex, 1);
      // debugger;

      }
    }

    // handleDelete(index, row) {
    //   console.log(index, row);
    // }
  }
};
</script>

<style>
</style>

<template>
  <div>
    <el-header v-if="save">
      <el-button size="small" style="float:right;" @click="saveData">save</el-button>
    </el-header>

    <el-header v-else>
      <el-row :gutter="30">
        <el-col :span="10">
          <el-select v-model="value" placeholder="请选择" size="small">
            <!-- <el-option
              v-for="item in options"
              :key="item.value"
              :label="item.label"
              :value="item.value"
            ></el-option>-->
          </el-select>
        </el-col>
        <el-col :span="8">
          <el-input size="small"></el-input>
        </el-col>

        <el-col :span="4">
          <el-button size="small">search</el-button>
        </el-col>
      </el-row>
    </el-header>

    <el-main>
      <el-table :data="data" border size="small">
        <!-- <el-table-column
          v-for="col in columns"
          :key="col.prop"
          :label="col.label"
          :prop="col.props"
        ></el-table-column>-->
        <!-- 借鉴错误写法 -->
        <el-table-column v-for="(col) in columns" :key="col.prop" v-bind="col"></el-table-column>
      </el-table>
    </el-main>
  </div>
</template>

<script>
// import { constants } from "crypto";
export default {
  name: "mapdata",
  props: {
    save: String,
    columns: Array,
    data: Array
  },
  data() {
    return {
      radioValue: "1",
      value: ""
    };
  },
  methods: {
    radioChange(e, row) {
      this.radioValue = e;
    },
    saveData() {
        console.log(456)
      this.$emit("handleData",'456');
    }
  }
};
</script>

<style>
</style>

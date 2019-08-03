<template>
  <div class="cell-double">
    <div style="display: 'inline-block'">
      <b>销售需求</b>
      <span>=</span>
      <el-select v-model="itemValue.select" placeholder="请选择" @change="selelctChange">
        <el-option v-for="(op,i) in options" :key="i" v-bind="op"></el-option>
      </el-select>
      <span>X</span>
      <el-input v-model="itemValue.double" @change="inputChange" style="width:30%;">
        <b slot="append">倍</b>
      </el-input>
    </div>
  </div>
</template>
<script>
export default {
  name: "cell-double",
  props: {
    options: {
      type: Array,
      required: true
    },
    value: Object
  },
  data() {
    return {
      itemValue: { select: "", double: "" }
    };
  },
  watch: {
    value: {
      handler: "fetchInit",
      immediate: true,
      deep: true
    }
  },
  created() {},
  methods: {
    fetchInit(val) {
      const { select, double } = val;
      this.itemValue.select = select;
      this.itemValue.double = double;
    },
    selelctChange(val) {
      this.itemValue.select = val;
      this.$emit("input", this.itemValue);
    },
    inputChange(val) {
      this.itemValue.double = val;
      this.$emit("input", this.itemValue);
    }
  }
};
</script>
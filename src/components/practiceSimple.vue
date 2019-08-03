<template>
  <el-tabs v-model="activeName" @tab-click="handleClick">
    <el-tab-pane label="用户管理" name="first">组件1</el-tab-pane>
    <el-tab-pane label="配置管理" name="second">组件2</el-tab-pane>
  </el-tabs>
</template>
<script>
export default {
  name: "good",
  data() {
    return {
      activeName: "second"
    };
  },
  props: {
    columns: {
      typr: Array
    },
    data: {
      typr: Array
    }
  },
  created() {
    console.log(this.data);
  },
  //   render(h) {
  //     return h("el-table", { props: Object.assign({}, this.$attrs, this.data) }, [
  //         this.showColumn(h, this.columns)
  //     ]);
  //   },
  methods: {
    handleClick(tab, event) {
      console.log(tab, event);
    }
  }
};
</script>

<style>
</style>

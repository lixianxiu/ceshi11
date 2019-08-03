<template>
  <div>
    <el-menu
      :default-active="activeIndex"
      class="el-menu-demo"
      mode="horizontal"
      @select="handleSelect"
    >
      <template v-for="item in data">
        <el-menu-item v-if="!item.children" :index="item.path" :key="item.hobby">{{item.title}}</el-menu-item>
        <template v-else >
          <el-submenu index="嵌套">
                <template v-if="item.children" slot="title">{{item.title}}</template>
                <el-menu-item :index="item.path" 
                 :key="item.hobby" 
                 v-for="item in item.children">{{item.title}}</el-menu-item>
          </el-submenu >
        </template>
      </template>
      <div class="line"></div>
    </el-menu>
    <!-- <el-menu :default-active="activeIndex" class="el-menu-demo" mode="horizontal" @select="handleSelect">
  <el-menu-item index="1">处理中心</el-menu-item>
  <el-submenu index="2">
    <template slot="title">我的工作台</template>
    <el-menu-item index="2-1">选项1</el-menu-item>
    <el-menu-item index="2-2">选项2</el-menu-item>
    <el-menu-item index="2-3">选项3</el-menu-item>
    <el-submenu index="2-4">
      <template slot="title">选项4</template>
      <el-menu-item index="2-4-1">选项1</el-menu-item>
      <el-menu-item index="2-4-2">选项2</el-menu-item>
      <el-menu-item index="2-4-3">选项3</el-menu-item>
    </el-submenu>
  </el-submenu>
  <el-menu-item index="3" disabled>消息中心</el-menu-item>
  <el-menu-item index="4"><a href="https://www.ele.me" target="_blank">订单管理</a></el-menu-item>
</el-menu>
    <div class="line"></div>-->
  </div>
</template>

<script>
export default {
  data() {
    return {
      activeIndex: "1",
      activeIndex2: "1",
      data: [
        {
          title: "one",
          hobby: "1",
          path: "qq.com"
        },
        {
          title: "one",
          hobby: "2",
          path: "qq2.com"
        },
        {
          title: "one",
          hobby: "3",
          path: "qq3.com"
        },
        {
          title: "two",
          hobby: "2",
          children: [
            {
              title: "消费者中心",
              path: "baidu.com",
              hobby: "3"
            },{
              title: "管理中心",
              path: "baidu.com",
              hobby: "4"
            }
          ]
        },{
          title: "one",
          hobby: "4",
          path: "qq4.com"
        },
      ]
    };
  },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    }
  }
};
</script>

<style>
</style>

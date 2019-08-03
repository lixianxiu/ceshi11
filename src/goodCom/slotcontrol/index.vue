<template>
  <div>
    <el-container>
      <el-row>
        <el-col>hello world</el-col>
      </el-row>
    </el-container>
    <slot name="seeMe" v-if="seen">
      <div>now you can see me!</div>
    </slot>
  </div>
</template>

<script>
export default {
  props: {
    seen: {
      required: true
    }
  }
};
</script>

<style>
</style>

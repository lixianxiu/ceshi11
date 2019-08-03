<template>
  <el-transfer
    v-model="value"
    :render-content="renderFunc"
    :props="{
      key: 'value',
      label: 'desc'
    }"
    :data="data"
  ></el-transfer>
</template>

<script>
export default {
  data() {
    const generateData = _ => {
      const data = [];
      for (let i = 1; i <= 15; i++) {
        data.push({
          value: i,
          desc: `备选项 ${i}`,
        //   disabled: i % 4 === 0
        });
      }
      return data;
    };
    return {
      data: generateData(),
      value: [],
      renderFunc: (h, option) => {
        return (
          <span>
            {option.value} - {option.desc}
          </span>
        );
      }
    };
  },
  created() {
    // console.log(this.data);
  }
};
</script>

<style>
</style>

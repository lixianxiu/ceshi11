<template>
  <div>I'am a simulationer!</div>
</template>

<script>
import api from "../axios/api.js";

export default {
  name: "Mock",
  data() {
    return {
      dataShow: []
    };
  },
  created() {
    this.getData();
  },
  methods: {
    async getData() {
      let res = await api.mockdata("/api");
      console.log(res);
      this.dataShow = res.data;
    }
  }
};
</script>

<style>
</style>

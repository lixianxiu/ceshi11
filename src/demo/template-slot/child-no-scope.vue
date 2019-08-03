<template>
  <div class="child">
    <slot></slot>
    <br />
    <slot name="bt" v-slot:data="params"></slot>
  </div>
</template>
<script>
export default {
  name: "child",
  data() {
    return {
      params: "123"
    };
  }
};
</script>



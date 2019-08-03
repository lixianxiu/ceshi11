<script>
export default {
  name: "render-slot-child",
  data() {
    return {};
  },
  render(h) {
    //作用域插槽
    const defaultSlots = this.$slots.default;
    //非作用域插槽
    const hasNameSlots = this.$slots["name1"];
    console.log(defaultSlots, "defaultSlots");
    console.log(hasNameSlots, "hasNameSlots");
    return h("div", [
      this.$scopedSlots.name1({ data: "456" }),
      // this.$slots["name1"]
      // this.$scopedSlots.name2({ data: "123" }),
      h('div',"i m slot down one information"),
      h('div',"i m slot down two information"),

      // defaultSlots({ data: "789" }),
      // this.$scopedSlots.name3({ data: "123" }),
      // this.$scopedSlots.name4({ data: "456" }),
      // this.$scopedSlots.name5({ data: "654" }),
      // this.$scopedSlots.name6({ data: "abc" }),
    ].concat(this.$slots.default));
  },
  mounted() {
    console.log(this.$scopedSlots, "scopedSlots");
    console.log(this.$slots);

  }
};
</script>




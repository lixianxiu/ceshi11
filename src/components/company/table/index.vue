

<script>
export default {
  name: "g-table",
  components: {
    "g-columns": () => import("./inner.vue")
  },
  props: {
    data: Array,
    columns: Array
  },
  render(h) {
    return h(
      "el-table",
      {
        props: Object.assign({}, this.$attrs, {
          data: this.data,
          border: true
        })
      },
      [h("g-columns", { props: { columns: this.columns, data: this.data } })]
    );
  }
};
</script>

<style>
</style>

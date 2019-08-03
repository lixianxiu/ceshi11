<script>
export default {
  name: "render-slot-parent",
  components: {
    child: () => import("./render-slot-child.vue")
  },
  data() {
    return {};
  },
  render(h) {
    return h("div", [
      h(
        "child",
        {
          class: { two: true },
          scopedSlots: {
            name1: scope => {
              return h("div", { class: { three: true } }, scope.data);
            }
           
          }
        },
        [h("div", {}, 12313421421)]
      )
    ]);
  }
};
</script>
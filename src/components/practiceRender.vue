
<script>
export default {
  name: "tablevue",
  props: {},
  data() {
    return {};
  },
  created() {
    console.log(666);
  },
  render(h) {
    return h("div", [this.showIt(h)]);
  },
  methods: {
    showIt(h) {
      return h(
        "div",
        {
          class: { name: true },
          style: { color: "blue" },
          attr: { id: "id_123" },
          domProps: {
            href: ".....hao123"
          },
          on: {
            click: () => {
              console.log(666);
            }
          }
        },
        // [h('span',{},'2'),h('span',{},'2'),h('span',{},'2'),h('span',{},'2'),h('span',{},'2')]
        [
          this.showMore(h, [
            { title: 1 },
            { title: 1 },
            { title: 1 },
            { title: 1 },
            { title: 1 },
            { title: 1 }
          ])
        ]
      );
    },
    showMore(h, ...params) {
      // console.log(params);
      return (
        params &&
        params[0].map(item => {
          // console.log(item);
          return h(
            "span",
            {
              props: Object.assign({}, this.$attrs, item)
            },
            [`${item.title}`]
          );
        })
      );
      // console.log(data);

      return data;
    }
  }
};
</script>

<style>
</style>

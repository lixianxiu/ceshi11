<script>
export default {
  name: "table-column",
  props: {
    columns: {
      type: Object,
      required: true
    }
  },
  data() {
    return {};
  },
  render(h) {
    return h("div", this.renderColumns(h, this.columns));
  },
  methods: {
    renderColumns(h, columns) {
      return (
        columns &&
        columns.map(col =>
          h(
            "el-table-column",
            {
              props: Object.assign({}, this.$attrs, col)
            },
            this.renderColumns(h, col.children)
          )
        )
      );
    }
  }
};

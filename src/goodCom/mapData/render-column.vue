<script>
export default {
  name: "render-column",
  props: {
    columns: Array
  },
  render(h) {
    return <div>{this.renderColumns(h, this.columns)}</div>;
  },
  methods: {
    renderColumns(h, columns) {
      return columns.map(col =>
        h("el-table-column", {
          props: col,
          scopedSlots: {
            default: scope => {
              const ele = "el-input";
              return h(ele, {
                props: {
                  value: scope.row[scope.column.property]
                }
              });
            }
          }
        })
      );
    }
  }
};
</script>

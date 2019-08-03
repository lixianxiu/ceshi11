
<script>
import { get, set } from "loadsh";
let len = 0;
export default {
  name: "table-column",
  props: {
    columns: {
      type: Array
    },
    data: Array
  },
  render(h) {
    return h("div", this.renderColumns(h, this.columns));
  },
  methods: {
    renderColumns(h, columns) {
      return (
        columns &&
        columns.map((col, index) => {
          console.log(col, "s", index);
          let columnIndex;
          len = col.children ? len : len + 1;
          columnIndex = len - 1;
          console.log("columnIndex", columnIndex);
          return h(
            "el-table-column",
            {
              props: Object.assign({}, this.$attrs, col),
              scopedSlots: {
                default: scope => {
                  const params = {
                    // roIndex: scope.$index,
                    // row: scope.row,
                    // columnIndex,
                    // prop: col.prop,
                    // column: scope.column
                  };
                  return get(scope.row, col.prop);
                }
              }
            }
            // this.renderColumns(h, col.children)
          );
        })
      );
    }
  }
};
</script>

<style>
</style>

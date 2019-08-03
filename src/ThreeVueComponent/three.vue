
<script>
export default {
  name: "table-column",
  props: {
    columns: {
      type: Array,
      required: true
    }
  },
  data() {
    return {};
  },
  render(h) {
    return <div>{this.renderColumns(h, this.columns)}</div>;
    // {...Object.assign({}, this.$attrs, col)}
  },
  methods: {
    renderColumns(h, columns) {
      return (
        columns &&
        columns.map(col => {
          return (
            <el-table-column {...{ props: col }}>
              {this.renderColumns(h, col.children)}
            </el-table-column>
          );
        })
      );
    }
  }
};

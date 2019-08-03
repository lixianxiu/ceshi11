
<script>
export default {
  name: "cell-double",
  props: {
    options: {
      type: Array,
      required: true
    },
    value: Object
  },
  data() {
    return {
      itemValue: { select: "", double: "" }
    };
  },
  watch: {
    value: {
      handler: "fetchInit",
      immediate: true,
      deep: true
    }
  },
  created() {},
  methods: {
    fetchInit(val) {
      const { select, double } = val;
      this.itemValue.select = select;
      this.itemValue.double = double;
    },
    selelctChange(val) {
      this.itemValue.select = val;
      this.$emit("input", this.itemValue);
    },
    renderOption(op) {
      return <el-option {...{ props: op }} />;
    },
    inputChange(val) {
      this.itemValue.double = val;
      this.$emit("input", this.itemValue);
    }
  },
  render(h) {
    return (
      <div style={{ display: "inline-block" }}>
        <b>销售需求</b>
        <span> = </span>
        <el-select
          value={this.itemValue.select}
          onChange={val => this.selelctChange(val)}
          placeholder="请选择"
        >
          {this.options.map(op => this.renderOption(op))}
        </el-select>
        <span>X</span>
        <el-input
          value={this.itemValue.double}
          style={{ width: "30%" }}
          onChange={val => this.inputChange(val)}
        >
          <b slot="append">倍</b>
        </el-input>
      </div>
    );
  }
};
</script>
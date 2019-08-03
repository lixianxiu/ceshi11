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
      handler: function(val) {
        const { select, double } = val;
        this.itemValue.select = select;
        this.itemValue.double = double;
      },
      immediate: true,
      deep: true
    }
  },
  created() {},
  render(h) {
    return h("span", {}, [
      h("b", "销售需求"),
      h("span", " = "),
      h(
        "el-select",
        {
          attrs: {
            placeholder: "请选择"
          },
          props: {
            value: this.itemValue.select
          },
          on: {
            input: val => {
              this.itemValue.select = val;
              this.$emit("input", this.itemValue);
            }
          }
        },
        this.options.map(op =>
          h("el-option", {
            props: {
              label: op.label,
              value: op.value
            }
          })
        )
      ),
      h("span", " X "),
      h(
        "el-input",
        {
          style: {
            width: "30%"
          },
          props: {
            value: this.itemValue.double
          },
          on: {
            input: val => {
              this.itemValue.double = val;
              this.$emit("input", this.itemValue);
            }
          }
        },
        [
          h(
            "div",
            {
              slot: "append"
            },
            "倍"
          )
        ]
      )
    ]);
  }
};

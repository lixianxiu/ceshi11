

<script>
import { format } from "path";
export default {
  name: "jsx-form",
  data() {
    return {
      show: true,
      ruleFrom: {
        age: ""
      },
      rules: {
        age: [
          {
            min: 3,
            max: 10,
            message: "请输入活动名称",
            trigger: "blur"
          }
        ]
      }
    };
  },
  render(h) {
    return this.jsxForm();
  },
  methods: {
    showIt() {
      this.show = this.show === "none" ? "block" : "none";
    },
    jsxForm() {
      return (
        <div>
          <el-form
            label-width={"100px"}
            model={this.ruleFrom}
            rules={this.rules}
            className="form-ss"
          >
            <el-form-item label={"your age:"} prop={"age"}>
              <el-input
                value={this.ruleFrom.age}
                onInput={val => {
                  this.ruleFrom.age = val;
                }}
              ></el-input>
            </el-form-item>
          </el-form>
        </div>
      );
    }
  }
};
</script>

<style >
</style>

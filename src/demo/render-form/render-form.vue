
<script>
import { debuglog } from "util";
import { constants } from "crypto";
export default {
  name: "render-form",
  data() {
    /***
     * validator way
     */
    var checkAge = (rule, value, callback) => {
      value = Number(value);
      const reg = /^[1-9]{1,3}$/;
      if (!reg.test(value)) {
        return callback(new Error("请输入年龄,必须是数字1-3位!"));
      }
      if (!value) {
        return callback(new Error("年龄不能为空"));
      }
      setTimeout(() => {
        if (!Number.isInteger(value)) {
          callback(new Error("请输入数字值"));
        } else {
          if (value < 18) {
            callback(new Error("必须年满18岁"));
          } else {
            callback();
          }
        }
      }, 10);
    };
    /**
     * data
     */
    return {
      ruleFrom: {
        age: ""
      },
      rules: {
        /***'
         * the rulues
         */
        age: [
          { required: true, trigger: "blur", message: "it is must to import " },
          { validator: checkAge, trigger: "blur" }
        ]
      }
    };
  },
  render(h) {
    return h("div", [this.vnodeFrom(h)]);
  },
  methods: {
    /**
     * VALIDATTOR FUNCTION,
     * formName : that's , you bind ref element;
     */
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        /**
         * the valid is a boolean
         */
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    /***
     * reset the form  you can use this method. all right
     */
    resetForm(formName) {
      this.$refs[formName].resetFields();
    },

    /**
     * constructed the template
     */
    vnodeFrom(h, params) {
      return h(
        "el-form",
        {
          props: {
            "label-width": "100px",
            model: this.ruleFrom,
            rules: this.rules
          },
          class: { "demo-ruleForm": true },
          ref: "ruleForm"
        },
        [
          h(
            "el-form-item",
            {
              props: {
                label: "Age",
                prop: "age"
              }
            },
            [
              h("el-input", {
                props: {
                  value: this.ruleFrom.age
                },
                on: {
                  input: val => {
                    this.ruleFrom.age = val;
                  }
                }
              })
            ]
          ),
          h(
            "el-button",
            {
              on: {
                click: e => {
                  this.submitForm("ruleForm");
                }
              }
            },
            "SUBMIT"
          )
        ]
      );
    }
  }
};
</script>

<style>
</style>

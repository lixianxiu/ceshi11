<template>
  <div>
    <el-form
      :model="numberValidateForm"
      ref="numberValidateForm"
      label-width="100px"
      class="demo-ruleForm"
      :rules="rules"
    >
      <el-form-item label="年龄" prop="age" :rules="[{min:1,max:2,message:'asd'}]">
        <el-input type="age" v-model.number="numberValidateForm.age" autocomplete="off"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('numberValidateForm')">提交</el-button>
        <el-button @click="resetForm('numberValidateForm')">重置</el-button>
      </el-form-item>
    </el-form>
  </div>
</template>

<script>
export default {
  data() {
    const validateAge = (rule, value, callback) => {
      if (value === "") {
        callback(new Error("请输入年龄"));
      } 
    };
    return {
      numberValidateForm: {
        age: "",
        checkAge:''
      },
      rules:{
          age:[{
              validator :validateAge ,tigger:'blur'
          }]
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          console.log("error submit!!");
          return false;
        }
      });
    },
    resetForm(formName) {
      this.$refs[formName].resetFields();
    }
  }
};
</script>
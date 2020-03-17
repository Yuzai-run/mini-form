<template>
  <div>
    <!-- <h2>element表单组件</h2>
    <el-form :model="ruleForm" :rules="rules" ref="ruleForm" label-width="100px">
      <el-form-item label="账号" prop="name">
        <el-input v-model="ruleForm.name"></el-input>
      </el-form-item>
      <el-form-item label="密码" prop="password">
        <el-input v-model="ruleForm.password"></el-input>
      </el-form-item>
      <el-form-item>
        <el-button type="primary" @click="submitForm('ruleForm')">提交</el-button>
      </el-form-item>
    </el-form> -->
    <h2>仿element表单组件</h2>
    <!-- <MiniInput label="账号" :value="ruleForm.name" @input="ruleForm.name = $event"></MiniInput> -->
    <mini-form :model="ruleForm" :rules="rules" ref="miniForm">
      <mini-form-item label="账号" prop="name">
        <mini-input v-model="ruleForm.name"></mini-input>
      </mini-form-item>
      <mini-form-item label="密码" prop="password">
        <mini-input type="password" v-model="ruleForm.password"></mini-input>
      </mini-form-item>
      <mini-form-item>
        <el-button type="primary" @click="submitForm('miniForm')">提交</el-button>
      </mini-form-item>
    </mini-form>
  </div>
</template>

<script>
import MiniForm from "./MiniForm.vue";
import MiniFormItem from "./MiniFormItem.vue";
import MiniInput from "./MiniInput.vue";
export default {
  components: {
    MiniInput,
    MiniFormItem,
    MiniForm
  },
  data() {
    return {
      ruleForm: {
        name: "",
        password: ""
      },
      rules: {
        name: [{ required: true, message: "请输入账号!", trigger: "blur" }],
        password: [
          { required: true, message: "请输入密码!", trigger: "blur" },
          { min: 3, max: 5, message: '长度在 3 到 5 个字符!', trigger: 'blur' }
        ]
      }
    };
  },
  methods: {
    submitForm(formName) {
      this.$refs[formName].validate(valid => {
        if (valid) {
          alert("submit!");
        } else {
          alert("error submit!!");
          return false;
        }
      });
    }
  }
};
</script>
<style  scoped>
*{
  margin: 10px;
}
</style>
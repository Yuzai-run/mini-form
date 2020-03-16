<template>
  <div>
    <label v-if="label" class="label">{{label}}</label>
    <!-- 插槽 -->
    <slot></slot>
    <!-- 校验错误信息 -->
    <p v-if="errorMessage" class="error">{{errorMessage}}</p>
  </div>
</template>

<script>
import Validate from "async-validator";
export default {
  inject: ["form"],
  props: {
    label: {
      type: String,
      default: ""
    },
    prop: {
      type: String
    }
  },
  data() {
    return {
      errorMessage: ""
    };
  },
  created() {
    this.$on("validate", this.validate);
  },
  methods: {
    validate() {
      return new Promise(resovle => {
        //校验规则制定
        const descriptor = {
          [this.prop]: this.form.rules[this.prop]
        };
        //创建校验器
        const validator = new Validate(descriptor);
        //执行校验
        validator.validate(
          {
            [this.prop]: this.form.model[this.prop]
          },
          error => {
            if (error) {
              this.errorMessage = error[0].message;
              resovle(false);
            } else {
              this.errorMessage = "";
              resovle(true);
            }
          }
        );
      });
    }
  }
};
</script>

<style scoped>
.error {
  color: red;
}
</style>
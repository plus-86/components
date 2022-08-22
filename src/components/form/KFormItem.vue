<template>
  <div>
    <!-- label -->
    <label v-if="label">{{ label }}</label>
    <slot> </slot>
    <!-- 校验信息的显示 -->
    <p v-if="error">{{ error }}</p>
  </div>
</template>

<script>
import Schema from 'async-validator' // 校验的库
export default {
  inject: ['form'], // 注入KForm实例，可以拿到从KForm注入的数据模型model
  mounted() {
    // 监听KInput派发的validate，当input框内容发生变化，进行内容校验
    this.$parent.$on('validate', () => {
      this.validate()
    })
  },
  methods: {
    validate() {
      // 当前规则
      const rules = this.form.rules[this.prop]
      // 当前值
      const value = this.form.model[this.prop]

      // 校验描述对象
      const desc = { [this.prop]: rules }
      const schema = new Schema(desc)
      return schema.validate({ [this.prop]: value }, (errors) => {
        if (errors) {
          this.error = errors[0].message
        } else {
          this.error = ''
        }
      })
    }
  },
  data() {
    return {
      error: '' // error是空，校验就是通过的
    }
  },
  props: {
    label: {
      type: String,
      default: ''
    },
    // 数据模型对应的key值
    prop: {
      type: String
    }
  }
}
</script>

<style lang="scss" scoped>
p {
  margin: 0;
  font-size: 12px;
  color: red;
}
</style>

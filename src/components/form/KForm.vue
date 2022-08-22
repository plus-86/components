<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
export default {
  // 提供KForm的实例，因为数据模型model是放到KForm里往下传的
  provide() {
    return {
      form: this
    }
  },
  props: {
    // 数据模型
    model: {
      type: Object,
      required: true // 必传
    },
    // 校验规则
    rules: {
      type: Object
    }
  },
  methods: {
    validate(cb) {
      // 获取所有KFormItem
      console.log(this.$children)
      debugger
      const tasks = this.$children
        .filter((item) => item.prop) // 过滤掉没有prop属性的item
        .map(
          (item) => item.validate() // [result]
        )
      // 统一处理所有promise结果

      Promise.all(tasks)
        .then(() => {
          cb(true) // 所有校验通过
        })
        .catch(() => cb(false)) // 有校验失败
    }
  }
}
</script>

<style></style>

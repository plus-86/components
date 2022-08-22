<template>
  <div>
    <slot></slot>
  </div>
</template>

<script>
export default {
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
      const tasks = this.$children
        .filter((item) => item.prop) // 过滤掉没有prop属性的item
        .map(
          (item) => item.validate() // [result]
        )
      // 统一处理所有promise结果

      Promise.all(tasks)
        .then(() => {
          cb(true)
        })
        .catch(() => cb(false))
    }
  }
}
</script>

<style></style>

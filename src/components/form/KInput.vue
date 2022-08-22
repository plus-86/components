<template>
  <div>
    <!-- 自定义组件双向绑定： value 、 @input -->
    <!-- v-bind="$attrs"的作用是展开$attrs -->
    <!-- 不在props内声明的attributes会被收纳到$attrs内，类似placeholder这类的attribute如果在props内过多声明，代码会显得冗余 -->
    <input v-bind="$attrs" :value="value" :type="type" @input="onInput" />
  </div>
</template>

<script>
export default {
  inheritAttrs: false, // 在子组件标签上的attributes如果没有在子组件的props内声明，则都会被继承到子组件最外层的div上，这个声明是用来取消继承attributes的
  props: {
    // 父组件通过v-model传来的prop 名为 value
    value: {
      type: String,
      default: ''
    },
    type: {
      type: String,
      default: 'text'
    }
  },
  methods: {
    onInput(e) {
      // 派发一个input事件即可。父组件触发子组件的input事件并附带新的值的时候会更新prop的value
      this.$emit('input', e.target.value)

      // 当数据变化后，通知父级执行校验
      this.$parent.$emit('validate') // 以KForm父组件做桥，KFormItem用this.$parent.$on('validate')监听，并执行回调
    }
  }
}
</script>

<style></style>

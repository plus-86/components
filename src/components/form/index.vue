<template>
  <div>
    <KForm :model="userInfo" :rules="rules" ref="loginForm">
      <!-- 用户名 -->
      <KFormItem prop="username" label="用户名">
        <!-- 这里的userInfo.username的值，将会传入名为value的prop给子组件。同时当 KInput 触发一个input事件并附带一个新的值的时候，这个userInfo.username的prop会更新-->
        <KInput placeholder="请输入用户名" v-model="userInfo.username"></KInput>
      </KFormItem>
      <!-- 密码 -->
      <KFormItem prop="password" label="密码">
        <KInput
          placeholder="请输入密码"
          type="password"
          v-model="userInfo.password"
        ></KInput>
      </KFormItem>
      <KFormItem>
        <button @click="login">登录</button>
      </KFormItem>
    </KForm>
  </div>
</template>

<script>
import KInput from '@/components/form/KInput.vue'
import KFormItem from '@/components/form/KFormItem.vue'
import KForm from '@/components/form/KForm.vue'
export default {
  data() {
    return {
      userInfo: {
        username: '',
        password: ''
      },
      rules: {
        username: [{ required: true, message: '请输入用户名' }],
        password: [{ required: true, message: '请输入密码' }]
      }
    }
  },
  methods: {
    login() {
      // 每次提交都调用KForm的校验方法validate
      this.$refs['loginForm'].validate((valid) => {
        if (valid) {
          alert('submit')
        } else {
          console.log('error submit!')
          return false
        }
      })
    }
  },
  components: {
    KInput,
    KFormItem,
    KForm
  }
}
</script>

<style></style>

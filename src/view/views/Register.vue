<template >
  <div >
    <van-form @submit="onSubmit" >
      <van-field
        v-model="username"
        name="username"
        label="用户名"
        placeholder="用户名"
        :rules="[{ required: true, message: '请填写用户名' }]"
      />
      <van-field
        v-model="password"
        type="password"
        name="password"
        label="密码"
        placeholder="密码"
        :rules="[{ required: true, message: '请填写密码' }]"
      />
      <van-field
        v-model="newPassword"
        type="password"
        name="newPassword"
        label="确认密码"
        placeholder="确认密码"
        :rules="[{ required: true, message: '请填写密码' }]"
      />
      <div style="margin: 16px;" >
        <van-button round block type="info" native-type="submit" >提交</van-button >
      </div >
    </van-form >
  </div >
</template >

<script >
  import { fetchRegister } from "../../api/user";

  export default {
    name: "Register",
    data() {
      return {
        username: '',
        password: '',
        newPassword: '',
      }
    },
    methods: {
      async onSubmit(data) {
        if (data.password !== data.newPassword) {
          this.$Toast('密码不一致')
          return;
        }
        let { status, message } = await fetchRegister(data)
        this.$Toast(message)
        if (status === 0) {
          this.$router.replace('/home/user')
        }
      }
    }
  }
</script >

<style lang="scss" scoped >

</style >
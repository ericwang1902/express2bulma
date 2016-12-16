<template>
<div id="login-modal" class="modal">
  <div class="modal-background"></div>
  <div class="modal-content" style="width:300px;">
    <div class="box">
      <h3 class="title is-4">System Login</h3>
      <p class="control has-icon">
        <input class="input" type="text" v-model="username" placeholder="Account">
        <i class="fa fa-user"></i>
      </p>
      <p class="control has-icon">
        <input class="input" type="password" v-model="password" placeholder="Password">
        <i class="fa fa-lock"></i>
      </p>
      <p class="control">
        <button class="button is-primary" @click="login()">Login</button>
      </p>
    </div>
  </div>
</div>
</template>
<script>
export default {
  data () {
    return {
      username: '',
      password: ''
    }
  },
  methods: {
    login () {
      // 处理登录环节
      this.$http.post('/login', {'username': this.username, 'password': this.password}).then(
        function (res) {
          console.log(res)
          if (res.body.authresult === true) {
            this.$store.commit('isAuth', true)
          } else {
            console.log('用户名或密码错误！')
            global.$fn.toast('danger', '用户名或密码错误！')
          }
        }, function (res) {

      })
    }
  }
}
</script>

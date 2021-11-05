<template>
  <div class='card p-4 rounded-plus bg-faded'>
    <div v-if='messenger'>
      <div :class="'alert alert-'+typeMessenger" role="alert" >
        {{messenger}}
      </div>
    </div>
    <form @submit.prevent='onLogin()'>
      <div class='form-group'>
        <label class='form-label' for='email'>Email</label>
        <input type='email' v-model='user.Email' name='Email' id='email' class='form-control form-control-lg'
               placeholder='your id or email' required>
      </div>
      <div class='form-group'>
        <label class='form-label' for='password'>Password</label>
        <input type='password' v-model='user.Password' name='Password' id='password'
               class='form-control form-control-lg' placeholder='password' required>
        <div class='invalid-feedback'>Sorry, you missed this one.</div>
        <div class='help-block'>Your password</div>
      </div>
      <div class='row no-gutters'>
        <div class='col-lg-6 pr-lg-1 my-2'>
          <button type='submit' class='btn btn-info btn-block btn-lg'>Sign in with <i class='fab fa-google'></i>
          </button>
        </div>
        <div class='col-lg-6 pl-lg-1 my-2'>
          <button id="'js-login-btn" type='submit' class='btn btn-danger btn-block btn-lg'>Secure login</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  layout: 'account-form-layout',
  data() {
    return {
      user: {
        Email: '',
        Password: ''
      },
      messenger:'',
      typeMessenger:'',
    }
  },
  methods: {
    async onLogin() {

      try {
        console.log(this.$auth.loggedIn);
        const response = await this.$auth.loginWith('local', {data: this.user})
        console.log(response)
        switch (response.data) {
          case 1:
            this.messenger = 'OK!';
            this.typeMessenger = 'success';
              await this.$router.push('/account');
            break;
          case 2:
            this.messenger = 'Bạn đang đăng nhập trên thiết bị khác';
            this.typeMessenger = 'danger';
            break;
          case 3:
            this.messenger = 'Sai tài khoản hoặc mật khẩu';
            this.typeMessenger = 'danger';
            break;
          default:
            this.messenger = 'Hệ thống lỗi!!!';
            this.typeMessenger = 'danger';
            break;
        }
      } catch (err) {
        console.log(err)
      }
    }
  }
}

</script>


<template>
  <div class='card p-4 rounded-plus bg-faded'>
    <!--                  @if(\Illuminate\Support\Facades\Session::has('message'))-->
    <!--                  <div class="alert alert-{{\Illuminate\Support\Facades\Session::get('style')}}" role="alert">-->
    <!--                    {!! \Illuminate\Support\Facades\Session::get('message') !!}-->
    <!--                  </div>-->
    <!--                  @endif-->
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
      checkLogin: 0,
      messenger:'',
      typeMessenger:'',
    }
  },
  methods: {
    async onLogin() {
      const uri = 'http://localhost:8000/api/account/login'
      this.checkLogin = await this.$axios.post(uri, this.user)
      switch (this.checkLogin.data) {
        case 1:
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

    }
  }
}

</script>


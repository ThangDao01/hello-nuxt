<template>
  <div>
    <div class='card p-4 rounded-plus bg-faded'>
      <!--      @if(\Illuminate\Support\Facades\Session::has('message'))-->
      <!--      <div class="alert alert-{{\Illuminate\Support\Facades\Session::get('style')}}" role='alert'>-->
      <!--        {{ \Illuminate\Support\Facades\Session::get('message') }}-->
      <!--      </div>-->
      <!--      @endif-->
      <form @submit.prevent='onRegister()'>
        <div class='form-group' >
          <label class='form-label' for='fullname'>Full name</label>
          <input type='text' v-model='user.fullName' id='fullname' name='fullName' class='form-control form-control-lg' required>
        </div>
        <div class='form-group'>
          <label class='form-label' for='username'>Username</label>
          <input type='text' v-model='user.userName' id='username' name='userName' class='form-control form-control-lg' required>
        </div>
        <div class='form-group'>
          <label class='form-label' for='email'>Email</label>
          <input type='email' v-model='user.email' id='email' name='email' class='form-control form-control-lg' required>
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
  </div>
</template>

<script>
export default {
  layout: 'account-form-layout',
  data() {
    return {
      user: {
        fullName: '',
        userName: '',
        email: ''
      }
    }
  },
  methods: {
    onRegister() {
      const uri = 'http://localhost:8000/api/account/register';
      this.$axios.post(uri, this.user).then((response) => {
        this.$router.push('/account/login');
      })
    }
  }
}
</script>


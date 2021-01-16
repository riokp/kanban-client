<template>

  <div>
    <div id="login-form" class="container">
      <form @submit.prevent="login">
        <div class="mb-3">
          <label class="form-label">Email address</label>
          <input v-model="loginData.email" type="email" class="form-control" placeholder="email address">
          <div id="emailHelp" class="form-text">We'll never share your email with anyone else.</div>
        </div>
        <div class="mb-3">
          <label class="form-label">Password</label>
          <input v-model="loginData.password" type="password" class="form-control" placeholder="password">
        </div>
        <button type="submit" class="btn btn-primary">Login</button>
        <button class="btn btn-secondary" @click.prevent="switchPage('register')">Cancel</button>
      </form>
    </div>
    <button v-google-signin-button="clientId" class="google-signin-button"> Continue with Google</button>
  </div>
  
</template>

<script>
import GoogleSignInButton from 'vue-google-signin-button-directive'
export default {
  name: "LoginForm",
  props: ["loginData","login","currentPage","switchPage"],
  directives: {
    GoogleSignInButton
  },
  data() {
    return {
      clientId: '896738878495-o85tsaaedg4jgvunib0mun4cdk1c6600.apps.googleusercontent.com'
    }
  },
  methods: {
    OnGoogleAuthSuccess (idToken) {
      // Receive the idToken and make your magic with the backend
      let id_token = idToken
      console.log(id_token);
      axios({
        method: 'POST',
        url: `https://stormy-tor-29734.herokuapp.com/googleSignIn`,
        data: {id_token: id_token}
      }).then(response => {
        console.log(response);
        localStorage.setItem(`access_token`,response.access_token)
      })
    },
    OnGoogleAuthFail (error) {
      console.log(error)
    }
  }
}
</script>

<style>
  .google-signin-button {
    color: white;
    background-color: red;
    height: 50px;
    font-size: 16px;
    border-radius: 10px;
    padding: 10px 20px 25px 20px;
    box-shadow: 0 4px 8px 0 rgba(0, 0, 0, 0.2), 0 6px 20px 0 rgba(0, 0, 0, 0.19);
  }
</style>
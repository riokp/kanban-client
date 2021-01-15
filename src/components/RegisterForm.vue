<template>

      <div class="container" id="register-form">
        <form @submit.prevent="register">
          <div class="mb-3">
            <label class="form-label">Name</label>
            <input v-model="registerData.name" type="text" class="form-control" placeholder="Your name">
          </div>
          <div class="mb-3">
            <label class="form-label">Email address</label>
            <input v-model="registerData.email" type="email" class="form-control" placeholder="Your email address">
          </div>
          <div class="mb-3">
            <label class="form-label">Password</label>
            <input v-model="registerData.password" type="password" class="form-control" placeholder="Your password">
            <div id="passwordHelp" class="form-text">Please input password between 8-20 characters</div>
          </div>
          <button type="submit" class="btn btn-primary">Register</button>
          <button class="btn btn-secondary" @click="switchPage('login')">Login</button>
          <!-- <button v-google-signin-button="clientId" class="google-signin-button"> Continue with Google</button> -->
        </form>
      </div>
  
</template>

<script>
export default {
  name: "LoginForm",
  props: ["registerData","register","switchPage","currentPage","onSignIn"]
}
</script>

<style>

</style>
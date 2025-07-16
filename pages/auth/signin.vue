<template>
  <div class="d-flex align-center justify-center" style="height: 100vh">
    <v-card width="500" class="pa-7 text-center">
      <h1 class="my=">Login Page</h1>

      <v-form>
        <v-text-field
          label="Email"
          outlined
          rounded
          prepend-inner-icon="mdi-email"
        ></v-text-field>
        <v-text-field
          label="Password"
          outlined
          rounded
          prepend-inner-icon="mdi-lock"
          type="password"
          
        ></v-text-field>
        <v-btn rounded color="primary" block>Login</v-btn>
        <div class="hr-sect my-5">OR</div>
        <v-btn color="error" @click = "signinwithGoogle()" class="text-capitalize" rounded block>
          <v-icon left>mdi-google</v-icon> Sign In with google
        </v-btn>
      </v-form>
    </v-card>
  </div>
</template>

<script>
export default {
  layout: "auth",
  middleware: "guest",
  methods:{
    signinwithGoogle() { 
      this.$auth.loginWith('google')
    }
  }
}
</script>

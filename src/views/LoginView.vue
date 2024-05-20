<template>
  <v-container class="fill-height"
    ><v-row align="center" justify="center">
      <v-col cols="12" sm="8" md="4">
        <v-card class="elevation-6">
          <v-toolbar color="purple">
            <v-toolbar-title class="title"
              >Log in to Your Account</v-toolbar-title
            >
          </v-toolbar>
          <v-card-text>
            <v-form @submit.prevent="login">
              <v-text-field
                v-model="username"
                label="Username"
                prepend-icon="mdi-account"
              />
              <v-text-field
                v-model="password"
                type="password"
                label="Password"
                prepend-icon="mdi-lock"
              />
              <v-btn type="submit" color="purple" class="btn">Login</v-btn>
              <v-alert v-if="error" type="error">{{ errorMessage }}</v-alert>
            </v-form>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row></v-container
  >
</template>
<script>
export default {
  name: "LoginView",
  data: () => ({
    username: "",
    password: "",
    error: false,
    errorMessage: "",
  }),
  methods: {
    login() {
      if (this.username === "example" && this.password === "password") {
        this.$router.push({ name: "WelcomeView" });
      } else {
        this.error = true;
        this.errorMessage = "Incorrect username/password";
      }
    },
  },
};
</script>
<style>
.title {
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: bold;
  word-spacing: -5px;
  font-family: "Courier New", Courier, monospace;
}
.btn {
  width: 100%;
  font-weight: bold;
  font-family: "Courier New", Courier, monospace;
}
.v-label {
  font-family: "Courier New", Courier, monospace;
}
</style>

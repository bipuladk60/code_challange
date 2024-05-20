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
    errorMessage: "Username/Password is incorrect.",
  }),
  methods: {
    login() {
      fetch("https://dummyjson.com/auth/login", {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({
          username: this.username,
          password: this.password,
        }),
      })
        .then((res) => res.json())
        .then((data) => {
          if (data.token) {
            this.$router.push({
              name: "WelcomeView",
              params: { userId: data.id },
            });
          } else {
            this.error = true;
            this.errorMessage = "Incorrect username/password";
          }
        })
        .catch((err) => {
          console.error("Error:", err);
          this.error = true;
          this.errorMessage = "Login failed due to server error.";
        });

      // do this if the api call doen't work
      //    if (this.username === "example" && this.password === "password") {
      //         this.$router.push({name: "WelcomePage"}).catch(err => {
      //             console.error("Router error:", err);
      //         });
      //     }
      //     else {
      //         this.error = true;
      //     }
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

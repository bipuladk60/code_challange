<template>
  <v-container>
    <h1>Welcome, user</h1>
    <v-btn @click="$router.push({ name: 'LoginView' })"
      ><v-icon left>mdi-logout</v-icon>Logout</v-btn
    >
  </v-container>
</template>
<script>
export default {
  name: "WelcomeView",
};
</script>
<style>
h1 {
  font-family: "Courier New", Courier, monospace;
  font-weight: bold;
  display: flex;
  justify-content: center;
  align-items: center;
  word-spacing: -5px;
}
.v-btn {
  font-family: "Courier New", Courier, monospace;
  font-weight: bold;
  color: white;
  background-color: red;
}
</style>

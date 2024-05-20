<template>
  <v-container>
    <h1>Welcome to you, {{ user.name }}!</h1>
    <v-avatar size="150">
      <img
        :src="user.avatar"
        alt="avatar"
        style="object-fit: contain; width: 100%; height: 100%"
      />
    </v-avatar>
    <p>Your hair color is: {{ user.hairColor }}</p>
    <v-btn @click="$router.push({ name: 'LoginPage' })">Log Out</v-btn>
  </v-container>
</template>
<script>
export default {
  name: "WelcomeView",
  data: () => ({
    user: {
      id: null,
      name: "",
      avatar: "",
      hairColor: "",
    },
  }),
  mounted() {
    this.fetchUserData();
  },
  methods: {
    fetchUserData() {
      const userId = this.$route.params.userId;
      fetch(`https://dummyjson.com/users/${userId}`)
        .then((res) => res.json())
        .then((data) => {
          this.user.id = data.id;
          this.user.name = data.firstName;
          this.user.avatar = data.image;
          this.user.hairColor = data.hair.color;
        })
        .catch((err) => {
          console.error("error:", err);
        });
    },
  },
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

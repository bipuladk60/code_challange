<template>
  <v-container class="fill-height">
    <v-row align="center" justify="center" class="fill-height">
      <v-card class="pa-4 card" elevation="4">
        <v-row align="center" no-gutters>
          <v-col cols="12" md="4">
            <v-avatar size="125" class="mx-auto">
              <img
                :src="user.avatar"
                alt="User avatar"
                style="object-fit: cover; width: 100%; height: 100%"
              />
            </v-avatar>
          </v-col>
          <v-col cols="12" md="8">
            <v-card-title class="text-h5 mb-2">
              Welcome, {{ user.firstName }}!
            </v-card-title>
            <v-card-text
              >Name: {{ user.firstName }} {{ user.lastName }}</v-card-text
            >
            <v-card-text class="mb-4"
              >Hair Color: {{ user.hairColor }}</v-card-text
            >
            <v-card-actions>
              <v-btn @click="$router.push({ name: 'LoginView' })" text>
                <v-icon left>mdi-logout</v-icon>
                Log Out
              </v-btn>
            </v-card-actions>
          </v-col>
        </v-row>
      </v-card>
    </v-row>
  </v-container>
</template>
<script>
export default {
  name: "WelcomeView",
  data: () => ({
    user: {
      id: null,
      firstName: "",
      lastName: "",
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
      fetch(`https://dummyjson.com/users/${userId}`, {
        method: "GET",
      }) //making a get request to the api
        .then((res) => res.json())
        .then((data) => {
          this.user.id = data.id;
          this.user.firstName = data.firstName;
          this.user.lastName = data.lastName;
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
.card {
  max-width: 90vw;
  font-family: "Courier New", Courier, monospace;
}
.v-btn {
  background-color: red;
  color: white;
}
</style>

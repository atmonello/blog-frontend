<template>
  <v-app-bar app flat>
    <v-btn tile to="/" plain nuxt exact large>Home</v-btn>
    <v-btn tile to="/articles" plain nuxt large>Posts</v-btn>
    <v-btn tile to="/about" plain nuxt large>About</v-btn>
    <v-spacer></v-spacer>
    <v-btn v-if="!isAuthenticated" tile plain nuxt to="/login">
      <v-icon>mdi-account</v-icon>
      &nbsp;Login
    </v-btn>
    <v-menu v-else open-on-hover offset-y>
      <template v-slot:activator="{ on, attrs }">
        <v-btn tile plain v-bind="attrs" v-on="on">
          <v-icon>mdi-account-check</v-icon>{{ loggedInUser.username }}</v-btn
        >
      </template>
      <v-list>
        <v-list-item>
          <v-btn tile v-bind="attrs" plain v-on="on" @click="logout">
            Logout
          </v-btn>
        </v-list-item>
      </v-list>
    </v-menu>
  </v-app-bar>
</template>

<script>
import { mapGetters } from "vuex";

export default {
  computed: {
    ...mapGetters(["isAuthenticated", "loggedInUser"]),
  },
  methods: {
    async logout() {
      await this.$auth.logout();
    },
  },
};
</script>

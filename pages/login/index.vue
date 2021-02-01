<template>
  <v-container>
    <h2 class="title has-text-centered">Log In</h2>
    <v-snackbar
      v-model="error"
      :timeout="2500"
      type="error"
      elevation="24"
      color="error"
      top
      right
    >
      {{ errorMsg }}
    </v-snackbar>

    <v-form @submit.prevent="login">
      <v-container fluid>
        <v-row>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="email"
              label="E-mail"
              prepend-icon="mdi-email"
            ></v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="password"
              prepend-icon="mdi-lock"
              :append-icon="togglePasswordVisible ? 'mdi-eye' : 'mdi-eye-off'"
              :type="togglePasswordVisible ? 'text' : 'password'"
              label="Password"
              @click:append="togglePasswordVisible = !togglePasswordVisible"
            ></v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col cols="12" md="4">
            <v-btn x-large type="submit">Login</v-btn>
          </v-col>
        </v-row>
      </v-container>
    </v-form>
  </v-container>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      password: "",
      error: false,
      errorMsg: null,
      togglePasswordVisible: false,
    };
  },
  methods: {
    async login() {
      this.error = false;
      this.errorMsg = null;
      try {
        await this.$auth.loginWith("local", {
          data: {
            identifier: this.email,
            password: this.password,
          },
        });
        this.$router.push("/");
      } catch (e) {
        this.error = true;
        this.errorMsg = e.response.data.message[0].messages[0].message;
      }
    },
  },
};
</script>

<template>
  <v-container>
    <v-snackbar v-model="success" timeout="2500" color="success" top right>{{
      successMsg
    }}</v-snackbar>
    <v-snackbar v-model="error" timeout="2500" color="error" top right>{{
      errorMsg
    }}</v-snackbar>
    <v-form @submit.prevent="register">
      <v-container fluid>
        <v-row fluid>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="username"
              prepend-icon="mdi-account"
              label="Username"
            ></v-text-field>
          </v-col>
        </v-row>
        <v-row fluid>
          <v-col cols="12" md="4">
            <v-text-field
              v-model="email"
              label="E-mail"
              prepend-icon="mdi-email"
              type="email"
            ></v-text-field>
          </v-col>
        </v-row>
        <v-row fluid>
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
        <v-row fluid>
          <v-col cols="12" md="4">
            <v-btn x-large type="submit">Register</v-btn>
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
      username: null,
      email: null,
      password: null,
      succcess: false,
      succcessMsg: null,
      error: false,
      errorMsg: null,
      togglePasswordVisibility: false,
    };
  },
  methods: {
    async register() {
      this.error = false;
      this.errorMsg = null;
      this.success = false;
      this.successMsg = null;

      try {
        this.$axios.setToken(false);

        await this.$axios.post("auth/local/register", {
          username: this.username,
          email: this.email,
          password: this.password,
        });

        this.success = true;
        this.succcessMsg =
          "A confirmation link has been sent to your email account.\nPlease click on the link to complete the registration process.";
      } catch (e) {
        this.error = true;
        this.errorMsg = e.response.data.message[0].messages[0].message;
      }
    },
  },
};
</script>

<template>
  <v-btn elevation="2" fab icon small fixed bottom left @click="setTheme">
    <v-icon>{{
      isDark ? "mdi-white-balance-sunny" : "mdi-weather-night"
    }}</v-icon>
  </v-btn>
</template>

<script>
export default {
  computed: {
    isDark() {
      return this.$vuetify.theme.dark === true;
    },
  },
  methods: {
    setTheme() {
      this.$vuetify.theme.dark = !this.$vuetify.theme.dark;
    },
  },
};
</script>

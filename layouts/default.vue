<template>
  <v-app dark>
    <AppToolbar />
    <v-main>
      <nuxt />
    </v-main>
    <AppDarkModeButton />
  </v-app>
</template>

<script>
import AppToolbar from "~/components/Navbar";
import AppDarkModeButton from "~/components/DarkModeButton";
import categoriesQuery from "~/apollo/queries/category/categories";

export default {
  components: {
    AppToolbar,
    AppDarkModeButton,
  },
  data() {
    return {
      categories: [],
    };
  },
  apollo: {
    categories: {
      prefetch: true,
      query: categoriesQuery,
    },
  },
};
</script>

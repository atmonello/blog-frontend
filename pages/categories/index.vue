<template>
  <v-container>
    <li v-for="category in categories" :key="category.id">
      {{ category.name }}
    </li>
  </v-container>
</template>
<script>
import categoriesQuery from "~/apollo/queries/category/categories";

export default {
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

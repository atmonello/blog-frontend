<template>
  <v-app dark>
    <v-main>
      <v-container>
        <ul>
          <li>
            <nuxt-link to="/">Home</nuxt-link>
          </li>
          <li>
            <nuxt-link to="/about">About</nuxt-link>
          </li>
          <li v-for="category in categories" :key="category.id">
            <nuxt-link
              :to="{ name: 'categories-id', params: { id: category.id } }"
              >{{ category.name }}
            </nuxt-link>
          </li>
        </ul>
        <nuxt />
      </v-container>
    </v-main>
  </v-app>
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

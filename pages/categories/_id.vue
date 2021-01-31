<template>
  <main>
    <div v-if="!!articles.length">
      <nuxt-link
        v-for="article in articles"
        :key="article.id"
        :to="{ name: 'articles-id', params: { id: article.id } }"
      >
        {{ article.title }}</nuxt-link
      >
    </div>
    <div v-else>
      <p>No articles found in this category.</p>
    </div>
  </main>
</template>

<script>
import categoryQuery from "~/apollo/queries/category/category";

export default {
  data() {
    return {
      category: {},
    };
  },
  computed: {
    name() {
      return this.category.name || null;
    },
    articles() {
      return this.category.articles || [];
    },
  },
  apollo: {
    category: {
      prefetch: true,
      query: categoryQuery,
      variables() {
        return { id: parseInt(this.$route.params.id) };
      },
    },
  },
};
</script>

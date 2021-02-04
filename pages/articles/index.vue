<template>
  <v-container class="flex flex-wrap">
    <v-card v-for="article in articles" :key="article.id">
      <v-img
        :src="`${apiUrl}${article.image.formats.small.url}`"
        height="180"
      ></v-img>
      <v-card-title class="text-h3"> {{ article.title }} </v-card-title>
      <v-card-text>
        <nuxt-link
          class="grey--text darken-2"
          :to="{ name: 'articles-id', params: { id: article.id } }"
          >Read more</nuxt-link
        >
      </v-card-text>
    </v-card>
  </v-container>
</template>

<script>
import articlesQuery from "~/apollo/queries/article/articles";

export default {
  data() {
    return {
      apiUrl: process.env.strapiBaseUri,
      articles: [],
    };
  },
  apollo: {
    articles: {
      prefetch: true,
      query: articlesQuery,
    },
  },
};
</script>

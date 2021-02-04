<template>
  <v-container>
    <v-row>
      <v-col cols="12">
        <span class="text-h2">{{ article.title }}</span>
      </v-col>
    </v-row>
    <v-divider class="my-8"></v-divider>
    <v-row>
      <v-col cols="12">
        <div v-html="this.$md.render(article.content)"></div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import articleQuery from "~/apollo/queries/article/article";

export default {
  data() {
    return {
      article: {
        content: "",
      },
    };
  },
  apollo: {
    article: {
      prefetch: true,
      query: articleQuery,
      variables() {
        return { id: parseInt(this.$route.params.id) };
      },
    },
  },
};
</script>

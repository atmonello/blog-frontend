<template>
  <v-container>
    <div v-html="this.$md.render(article.content)"></div>
  </v-container>
</template>

<script>
import articleQuery from "~/apollo/queries/article/article";

export default {
  data() {
    return {
      article: {},
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

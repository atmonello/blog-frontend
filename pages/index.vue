<template>
  <v-container>
    <v-row justify="center" class="mx-16 text-center">
      <v-col cols="12" class="mt-10">
        <h1 class="text-h1">André Monello</h1>
        <h2 class="text-h4 font-weight-light">
          Web Developer based in São Paulo, Brasil
        </h2>
      </v-col>
      <v-col cols="12">
        <v-icon>mdi-language-javascript</v-icon>
        <v-icon>mdi-vuejs</v-icon>
        <v-icon>mdi-nodejs</v-icon>
        <v-icon>mdi-language-html5</v-icon>
        <v-icon>mdi-language-css3</v-icon>
      </v-col>
    </v-row>
    <v-row class="px-16">
      <v-col cols="12">
        <v-timeline reverse align-top class="home__timeline">
          <v-timeline-item
            v-for="job in jobsByDate"
            :key="job.id"
            color="grey"
            fill-dot
          >
            <v-card>
              <v-card-title>
                <span class="text-h5">{{ job.company }}</span>
                <v-spacer></v-spacer>
                <span class="text-subtitle-1 font-weight-thin">{{
                  formatDate(job.start)
                }}</span>
                <span
                  v-if="job.finish"
                  class="text-subtitle-1 font-weight-thin"
                >
                  &nbsp;-
                  {{ formatDate(job.finish) }}</span
                >
                <span v-else class="text-subtitle-1 font-weight-thin">
                  &nbsp;- Current</span
                >
              </v-card-title>
              <v-divider inset></v-divider>
              <v-card-text>
                {{ job.description }}
              </v-card-text>
            </v-card>
          </v-timeline-item>
        </v-timeline>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import jobsQuery from "~/apollo/queries/job/jobs";

export default {
  data() {
    return {
      jobs: [],
    };
  },
  apollo: {
    jobs: {
      prefetch: true,
      query: jobsQuery,
    },
  },
  computed: {
    jobsByDate() {
      const _jobs = this.jobs;
      return _jobs.sort((a, b) => {
        if (a.start > b.start) return -1;
        else if (b.start > a.start) return 1;
        else return 0;
      });
    },
  },
  methods: {
    formatDate(date) {
      return this.$dateFns.format(new Date(date), "MM-yyyy");
    },
  },
};
</script>

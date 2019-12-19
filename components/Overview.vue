<template>
    <v-row>
      <v-col class="challenge" cols="3" v-for="page in challenges()">
          <ChallengeSummary :page="page"></ChallengeSummary>
      </v-col>
    </v-row>
</template>

<script>

import ChallengeSummary from '@theme/components/ChallengeSummary.vue'

export default {
  components: {
    ChallengeSummary
  },
  methods: {
    challenges() {
      // Refactor to config !
      const difficulties = ['easy', 'medium', 'hard', 'expert'];
      const exclusions = ['/'];

      return this.$site.pages
      .filter((page) => !exclusions.includes(page.path))
      .filter((page) => !page.frontmatter.draft)
      .sort((a, b) => {
        const aDifficulty = (a.frontmatter.difficulty || difficulties[0]).toLowerCase();
        const bDifficulty = (b.frontmatter.difficulty || difficulties[0]).toLowerCase();
        return difficulties.indexOf(aDifficulty) - difficulties.indexOf(bDifficulty);
      })
    }
  },
}
</script>

<style scoped>
</style>>

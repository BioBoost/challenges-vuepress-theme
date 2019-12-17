<template>
    <v-row>
      <v-col class="challenge flex-grow-0" v-for="page in challenges()">
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
      return this.$site.pages
      .filter((page) => page.path.startsWith("/challenges/"))
      // .filter((page) => !page.frontmatter.draft )
      // .sort((a, b) => {
      //   return a.frontmatter.semester - b.frontmatter.semester
      // })
    }
  },
}
</script>

<style scoped>
</style>>

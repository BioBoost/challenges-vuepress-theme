<template>
  <div>
    <v-app-bar
      color="red darken-2"
      dark
    >
      <v-toolbar-title>{{ $site.title }}</v-toolbar-title>

    </v-app-bar>
  </div>
</template>

<script>
export default {
  mounted: function() {
    // TODO: add this.$site.themeConfig.nav links to navbar
    // console.log(this.$site)
  }
}
</script>
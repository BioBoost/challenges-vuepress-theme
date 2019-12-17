<template>
  <v-app light>
    <v-content>
      <NavBar/>
      <v-container>
        <v-row justify="center">
          <v-col sm="4" lg="2">
            <v-img src="/images/logo.png" alt="DevBit logo" contain />
          </v-col>
        </v-row>
        <Content />
      </v-container>
    </v-content>
  </v-app>
</template>

<script>

import NavBar from '@theme/components/Navbar.vue'

export default {
  name: 'layout',
  components: {
    NavBar
  },
}
</script>

<style>
  .header-anchor {
    display: none;
  }
</style>
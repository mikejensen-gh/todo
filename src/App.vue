<template>
  <div id="app">
    <v-app dark>
      <v-content>
        <v-toolbar dark color="grey darken-3">
          <v-toolbar-title class="white--text">Todo manager v0.1.0</v-toolbar-title>

          <v-spacer></v-spacer>

          <v-btn icon @click="openInNewTab('https://github.com/mikejensen-gh/todo')">
            <v-icon>mdi-github-circle</v-icon>
          </v-btn>
        </v-toolbar>
        <v-container fluid fill-height>
          <v-layout justify-center>
            <v-flex  sm10 md9 lg8 xl6>
              <router-view></router-view>
            </v-flex>
          </v-layout>
        </v-container>
      </v-content>
    </v-app>
  </div>
</template>

<script>
export default {
  name: 'App',

  methods: {
    openInNewTab: function (url) {
      window.open(url, '_blank')
    }
  }
}
</script>

<style>
</style>

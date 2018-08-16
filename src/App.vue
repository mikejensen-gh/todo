<template>
  <div id="app">
    <v-app dark>
      <v-content>
        <v-toolbar dark color="grey darken-3" app>
          <v-toolbar-title class="white--text">Todo manager v0.1.0</v-toolbar-title>

          <v-spacer></v-spacer>

          <v-btn icon @click="openInNewTab('https://github.com/mikejensen-gh/todo')">
            <v-icon>mdi-github-circle</v-icon>
          </v-btn>
        </v-toolbar>
        <v-container fluid fill-height>
          <v-layout justify-center>
            <v-flex  sm10 md8 lg6>
              <router-view></router-view>
            </v-flex>
          </v-layout>

          <v-footer app class="pa-3">
            <v-layout row justify-space-between>
              <v-flex xs4 text-xs-left>
                <span>Breakpoint: <span class="hidden-sm-and-up">xs</span>
                  <span class="hidden-md-and-up hidden-xs-only">small</span>
                  <span class="hidden-lg-and-up hidden-sm-and-down">medium</span>
                  <span class="hidden-xl-only hidden-md-and-down">large</span>
                  <span class="hidden-lg-and-down">extra large</span>
                </span>
              </v-flex>

              <v-flex xs4 text-xs-center v-resize="onResize">
                  {{ windowSize }}
              </v-flex>

              <v-flex xs4 text-xs-right>
                <div>M Jensen &copy; {{ new Date().getFullYear() }}</div>
              </v-flex>
            </v-layout>
          </v-footer>
        </v-container>
      </v-content>
    </v-app>
  </div>
</template>

<script>
export default {
  name: 'App',

  data () {
    return {
      windowSize: ''
    }
  },

  methods: {
    openInNewTab: function (url) {
      window.open(url, '_blank')
    },

    onResize () {
      this.windowSize = `${window.innerWidth} x ${window.innerHeight} px`
    }
  },

  mounted () {
    this.onResize()
  },
}
</script>

<style>
</style>

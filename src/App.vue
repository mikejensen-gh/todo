<template>
  <div id="app">
    <v-app>
      <v-content>
        <v-toolbar dark color="primary">
          <v-toolbar-title class="white--text">Todo manager v0.1.0</v-toolbar-title>
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
  name: 'App'
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

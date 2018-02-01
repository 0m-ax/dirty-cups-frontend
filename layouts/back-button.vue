<template>
  <v-app dark>
    <v-toolbar fixed app >
      <v-btn icon class="hidden-xs-only" href="/">
        <v-icon>arrow_back</v-icon>
      </v-btn>
      <v-toolbar-title v-text="title" href="/"></v-toolbar-title>
    </v-toolbar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
    <v-footer app>
      <span>&copy; {{(new Date(Date.now())).getFullYear()}}</span>
    </v-footer>
  </v-app>
</template>

<script>
  export default {
    data () {
      return {
        title: 'Dirty Cups'
      }
    }
  }
</script>
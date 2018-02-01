<template>
  <v-app dark>
    <v-toolbar fixed app >
      <v-toolbar-title v-text="title" href="/"></v-toolbar-title>
    </v-toolbar>
    <v-content>
      <v-container>
        <nuxt />
      </v-container>
    </v-content>
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

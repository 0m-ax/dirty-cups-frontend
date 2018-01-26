<template>
  <v-app dark>
    <v-toolbar fixed app >
      <v-toolbar-title v-text="title"></v-toolbar-title>
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
        items: [
          { icon: 'list', title: 'Reports', to: '/' },
          { icon: 'report', title: 'Submit Report', to: '/submit' }
        ],
        title: 'Dirty Cups'
      }
    }
  }
</script>

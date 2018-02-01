<template>
  <v-layout row wrap>
    <v-flex xs12>
      <v-text-field
        v-model="searchText"
        lable="Phonenumber, username, email"
      ></v-text-field>
      <v-btn block @click="search">search</v-btn>
    </v-flex>
    <v-flex xs12>
      <v-list v-if="items.length > 0">
        <template v-for="item in items">
          <v-list-tile v-bind:key="item.title" :href="'/report/'+item.id">
            <v-list-tile-action>
              <v-icon>{{item.icon}}</v-icon>
            </v-list-tile-action>
            <v-list-tile-content>
              <v-list-tile-title v-html="item.title"></v-list-tile-title>
            </v-list-tile-content>
          </v-list-tile>
        </template>
      </v-list>
      <v-btn
        dark
        fixed
        bottom
        right
        fab
        color='purple'
        href='/report'
      >
        <v-icon>add</v-icon>
      </v-btn>
      </v-flex>
  </v-layout>
</template>
<script>
  import axios from 'axios'
  export default {
    layout:'back-button',
    methods: {
      search(){
        axios.post('http://dirty-cups.dev.maxc.in/report/searchReportsByContactHandle', {
          report: {
            handle: this.searchText
          }
        })
          .then((resp) => resp.data)
          .then((reports) => {
            this.items = reports.map((report) => {
                return {
                  icon: report.workTypeID === 'in-call' ? 'home' : report.workTypeID === 'street' ? 'directions_car' : 'hotel',
                  title: (report.workTypeID === 'in-call' ? 'In Call' : report.workTypeID === 'street' ? 'Street' : 'Out Call') + '',
                  id: report.reportID
                }
              })
          })
      }
    },
    data () {
      return {
        items: [],
        searchText:''
      }
    }
  }
</script>
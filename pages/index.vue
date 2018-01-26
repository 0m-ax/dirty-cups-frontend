<template>
  <v-layout>
    <v-flex xs12 sm12 md12>
    <v-list>
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
    data () {
      return {
        items: [
          { icon: 'home', title: 'Indoor', subtitle: '/', id: '1' },
          { icon: 'directions_car', title: 'Street', subtitle: '/', id: '2' },
          { icon: 'hotel', title: 'Outcall', subtitle: '/', id: '3' }
        ]
      }
    },
    asyncData () {
      return axios.post('http://dirty-cups.dev.maxc.in/report/searchReportsByContactHandle', {
        report: {
          handle: 'meme'
        }
      })
        .then((resp) => resp.data)
        .then((reports) => {
          return {
            items: reports.map((report) => {
              return {
                icon: report.workTypeID === 'in-call' ? 'home' : report.workTypeID === 'street' ? 'directions_car' : 'hotel',
                title: (report.workTypeID === 'in-call' ? 'In Call' : report.workTypeID === 'street' ? 'Street' : 'Out Call') + '',
                id: report.reportID
              }
            })
          }
        })
    }
  }
</script>
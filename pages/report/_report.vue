<template>
  <v-layout>
    <v-flex xs12 sm12 md12>
      <h1>Report</h1>
      <h2>WorkType</h2>
      {{report.workTypeID}}
      <h2>Region</h2>
      {{report.regionID}}
      <h2>Gender:</h2>
      {{report.genderID}}
      <h2>Contacts</h2> 
      <v-list two-line>
          <v-list-tile v-for="contact in report.contacts"  v-bind:key="contact.contactTypeID+contact.handle">
            <v-list-tile-content>
              <v-list-tile-title v-html="contact.contactTypeID"></v-list-tile-title>
              <v-list-tile-sub-title v-html="contact.handle"></v-list-tile-sub-title>
            </v-list-tile-content>
          </v-list-tile>
      </v-list>
    </v-flex>
  </v-layout>
</template>
<script>
import axios from 'axios'
export default {
  layout: 'back-button',
  data () {
    return {
      back: true,
      report: {
      }
    }
  },
  asyncData ({params}) {
    return axios.get('http://dirty-cups.dev.maxc.in/report/getByReportID/' + params.report)
      .then((resp) => resp.data)
      .then((report) => {
        return {
          report: report
        }
      })
  }
}
</script>
<template>
  <v-layout>
    <v-flex xs12 sm12 md12>
        {{workTypes}}
        <v-select
            v-bind:items="workTypes"
            v-model="select"
            label="Select"
            single-line
            item-text="name"
            item-value="workTypeID"
            return-object
        ></v-select>
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
      },
      workTypes: [],
      genders: [],
      regions: [],
      contactTypes: [],
      select: ''
    }
  },
  asyncData ({params}) {
    return Promise.all([
      axios.get('http://dirty-cups.dev.maxc.in/workType/getAll/' + params.report).then((resp) => resp.data),
      axios.get('http://dirty-cups.dev.maxc.in/gender/getAll/' + params.report).then((resp) => resp.data),
      axios.get('http://dirty-cups.dev.maxc.in/region/getAll/' + params.report).then((resp) => resp.data),
      axios.get('http://dirty-cups.dev.maxc.in/contactType/getAll/' + params.report).then((resp) => resp.data)
    ])
      .then(([workTypes, genders, regions, contactTypes]) => {
        return {
          workTypes,
          genders,
          regions,
          contactTypes
        }
      })
  }
}
</script>
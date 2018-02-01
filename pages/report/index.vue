<template>
  <v-layout>
    <v-flex xs12 sm12 md12>
        <v-form v-model="valid" ref="form">
            <p>
              How where you working when the time waster contacted you?
            </p>
            <v-select
                v-bind:items="workTypes"
                v-model="report.workTypeID"
                label="Work Type"
                single-line
                item-text="name"
                item-value="workTypeID"
                required
            ></v-select>
            <p>
              What gender where you working as when the time waster contacted you?
            </p>
            <v-select
                v-bind:items="genders"
                v-model="report.genderID"
                label="Gender"
                single-line
                item-text="name"
                item-value="genderID"
                required
            ></v-select>
            <p>
              What region where you working in at the time of the time waster contacted you?
            </p>
            <v-select
                autocomplete
                v-bind:items="regions"
                v-model="report.regionID"
                label="Region"
                single-line
                item-text="name"
                item-value="regionID"
                required
            ></v-select>
            <p>
              What are the time wasters contact details they contacted you with?
            </p>
            <v-container
            fluid
            grid-list-lg
            >
                <v-layout row wrap>
                    <v-flex xs12 v-for="(item, index) in report.contacts" :key="index">
                        <v-card>
                            <v-card-text>
                                <v-layout row wrap>
                                  <v-flex xs12 sm4>
                                    <v-select
                                        v-bind:items="contactTypes"
                                        v-model="report.contacts[index].contactTypeID"
                                        label="Contact Type"
                                        single-line
                                        item-text="name"
                                        item-value="contactTypeID"
                                        required
                                    ></v-select>
                                  </v-flex>
                                  <v-flex xs12 sm8>
                                    <v-text-field
                                        :disabled="!contactTypesObj[report.contacts[index].contactTypeID]"
                                        :label="contactTypesObj[report.contacts[index].contactTypeID]?contactTypesObj[report.contacts[index].contactTypeID].handleName:'handle'"
                                        v-model="report.contacts[index].handle"
                                        required
                                    ></v-text-field>
                                  </v-flex>
                                </v-layout>
                                <v-btn block @click="remove(index)">Remove</v-btn>
                            </v-card-text>
                        </v-card>
                    </v-flex>
                    <v-flex xs12>
                        <v-btn block @click="add()">Add contact</v-btn>
                    </v-flex>
                </v-layout>
            </v-container>
            <v-btn block @click="submit">Submit</v-btn>
        </v-form>
    </v-flex>
  </v-layout>
</template>
<script>
import axios from "axios";
export default {
  layout: "back-button",
  methods: {
    add(){
      this.report.contacts.push({contactTypeID:'',handle:''})
    },
    remove(index) {
      this.report.contacts.splice(index, 1);
      if(!this.report.contacts.length > 0){
        this.add()
      }
    },
    submit() {
      console.log(this.valid,this.$refs.form.validate())
      if (this.valid) {
        axios.post("http://dirty-cups.dev.maxc.in/report/create/", {
          report: {
            regionID: this.report.regionID,
            genderID: this.report.genderID,
            time: new Date(),
            workTypeID: this.report.workTypeID,
            contacts: this.report.contacts
          }
        });
      }
    }
  },
  data() {
    return {
      back: true,
      valid: false,
      contactTypesObj: {},
      report: {
        workTypeID: null,
        genderID: null,
        regionID: null,
        contacts: [
          {
            contactTypeID: "",
            handle: ""
          }
        ]
      },
      workTypes: [],
      genders: [],
      regions: [],
      contactTypes: [],
      select: ""
    };
  },
  asyncData({ params }) {
    return Promise.all([
      axios
        .get("http://dirty-cups.dev.maxc.in/workType/getAll/" + params.report)
        .then(resp => resp.data),
      axios
        .get("http://dirty-cups.dev.maxc.in/gender/getAll/" + params.report)
        .then(resp => resp.data),
      axios
        .get("http://dirty-cups.dev.maxc.in/region/getAll/" + params.report)
        .then(resp => resp.data),
      axios
        .get(
          "http://dirty-cups.dev.maxc.in/contactType/getAll/" + params.report
        )
        .then(resp => resp.data)
    ]).then(([workTypes, genders, regions, contactTypes]) => {
      let contactTypesObj = {};
      for (let contactType of contactTypes) {
        contactTypesObj[contactType.contactTypeID] = contactType;
      }
      return {
        workTypes,
        genders,
        regions,
        contactTypes,
        contactTypesObj
      };
    });
  }
};
</script>
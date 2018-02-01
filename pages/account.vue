<template>
  <v-layout row wrap>
    <v-flex xs12>
      <v-btn block @click="dialog=true">Delete Account</v-btn>
      <v-dialog v-model="dialog" persistent max-width="500px">
        <v-card>
          <v-card-title>
            <span class="headline">Delete Account</span>
          </v-card-title>
          <v-card-text>
            <v-container grid-list-md>
              <v-layout wrap>
                <v-flex xs12>
                  <v-text-field label="Password" hint="Enter your password to confirm deletion"></v-text-field>
                </v-flex>
              </v-layout>
            </v-container>
            <small>*indicates required field</small>
          </v-card-text>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn color="blue darken-1" flat @click.native="dialog = false">Close</v-btn>
            <v-btn flat @click.native="dialog = false">Delete account</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data: () => ({
    dialog:false
  }),
  methods: {
    changePassword() {

    },
    deleteAccount(){

    }
  }
};
</script>

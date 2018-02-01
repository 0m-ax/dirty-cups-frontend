<template>
    <v-flex> 
        <v-tabs fixed centered v-model="tab">
        
            <v-tabs-bar style="background-color: #212121;" dark>
                <v-tabs-slider color="purple"></v-tabs-slider>
                <v-tabs-item href="#signup-tab"> Signup</v-tabs-item>
                <v-tabs-item href="#login-tab">login</v-tabs-item>
            </v-tabs-bar>

            <v-tabs-items>
                <v-tabs-content id="signup-tab">
                    <v-card flat>
                        <v-form v-model="valid" ref="form" lazy-validation>

                            <v-text-field label="E-mail" v-model="email" :rules="emailRules" required></v-text-field>
                            <v-text-field label="Password" v-model="password" :rules="passwordRules" required></v-text-field>
                            <v-btn @click="signup" :disabled="!valid">Signup</v-btn>
                        </v-form>
                    </v-card>
                </v-tabs-content>

                <v-tabs-content id="login-tab">
                    <v-card flat>
                        <v-form v-model="valid" ref="form" lazy-validation>
                            <v-text-field label="E-mail" v-model="email" :rules="emailRules" required></v-text-field>
                            <v-text-field label="Password" v-model="password" :rules="passwordRules" required></v-text-field>
                            <v-btn @click="login" :disabled="!valid">login</v-btn>
                        </v-form>
                    </v-card>
                </v-tabs-content>
            </v-tabs-items>
        </v-tabs>
    </v-flex>
</template>

<script>
  import axios from 'axios'
export default {
  data: () => ({
    valid: true,
    tab:'',
    email: "",
    emailRules: [
      v => !!v || "E-mail is required",
      v =>
        /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(v) ||
        "E-mail must be valid"
    ],
    valid: true,
    password: "",
    passwordRules: [
      v => !!v || "Name is required",
      v => (v && v.length >= 10) || "Name must be greater than 10 characters"
    ]
  }),
  methods: {
    signup() {
      if (this.$refs.form.validate()) {
        axios.post("http://dirty-cups.dev.maxc.in/user/signup", {
          email: this.email,
          password: this.password
        }).then((resp)=>{
          if(resp.status !== 200){
            throw new Error(resp.data.message)
          }
          this.tab = 'login-tab'
          return resp.data;
        })
      }
    },
    login() {
      if (this.$refs.form.validate()) {
        axios.post("http://dirty-cups.dev.maxc.in/user/login", {
          email: this.email,
          password: this.password
        }).then((resp)=>{
          if(resp.status !== 200){
            throw new Error(resp.data.message)
          }
          this.tab = 'signup-tab'
          return resp.data;
        })
      }
    }
  }
};
</script>
<template>
    <v-flex> 
        <v-tabs fixed centered>

            <v-tabs-bar style="background-color: #212121;" dark>
                <v-tabs-slider color="purple"></v-tabs-slider>
                <v-tabs-item href="'#tab-1"> Signup</v-tabs-item>
                <v-tabs-item href="'#tab-2">Sign In</v-tabs-item>
            </v-tabs-bar>

            <v-tabs-items>
                <v-tabs-content id="'tab-1">
                    <v-card flat>
                        <v-form v-model="valid" ref="form" lazy-validation>

                            <v-text-field label="E-mail" v-model="email" :rules="emailRules" required></v-text-field>
                            <v-text-field label="Password" v-model="password" :rules="passwordRules" required></v-text-field>
                            <v-btn @click="signup" :disabled="!valid">Signup</v-btn>
                        </v-form>
                    </v-card>
                </v-tabs-content>

                <v-tabs-content id="'tab-2">
                    <v-card flat>
                        <v-form v-model="valid" ref="form" lazy-validation>
                            <v-text-field label="E-mail" v-model="email" :rules="emailRules" required></v-text-field>
                            <v-text-field label="Password" v-model="password" :rules="passwordRules" required></v-text-field>
                            <v-btn @click="login" :disabled="!valid">Sign in</v-btn>
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
        axios.post("/api/signup", {
          email: this.email,
          password: this.password
        });
      }
    },
    login() {
      if (this.$refs.form.validate()) {
        axios.post("api/login", {
          email: this.email,
          password: this.password
        });
      }
    }
  }
};
</script>
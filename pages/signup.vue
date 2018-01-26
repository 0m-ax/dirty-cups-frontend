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
                            <v-btn @click="submit" :disabled="!valid">Signup</v-btn>
                        </v-form>
                    </v-card>
                </v-tabs-content>

                <v-tabs-content id="'tab-2">
                    <v-card flat>
                        <v-form v-model="valid" ref="form" lazy-validation>
                            <v-text-field label="E-mail" v-model="email" :rules="emailRules" required></v-text-field>
                            <v-text-field label="Password" v-model="password" :rules="passwordRules" required></v-text-field>
                            <v-btn @click="submit" :disabled="!valid">Sign in</v-btn>
                        </v-form>
                    </v-card>
                </v-tabs-content>
            </v-tabs-items>
        </v-tabs>
    </v-flex>
</template>

<script>
export default {
  data: () => ({
    valid: true,
    name: "",
    nameRules: [
      v => !!v || "Name is required",
      v => (v && v.length <= 10) || "Name must be less than 10 characters"
    ],
    email: "",
    emailRules: [
      v => !!v || "E-mail is required",
      v =>
        /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(v) ||
        "E-mail must be valid"
    ],
    select: null,
    items: ["Item 1", "Item 2", "Item 3", "Item 4"],
    checkbox: false
  }),
  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        // Native form submission is not yet supported
        axios.post("/api/submit", {
          name: this.name,
          email: this.email,
          select: this.select,
          checkbox: this.checkbox
        });
      }
    },
    clear() {
      this.$refs.form.reset();
    }
  }
};
</script>

<script>
export default {
  data: () => ({
    valid: true,
    name: "",
    nameRules: [
      v => !!v || "Name is required",
      v => (v && v.length <= 10) || "Name must be less than 10 characters"
    ],
    email: "",
    emailRules: [
      v => !!v || "E-mail is required",
      v =>
        /^\w+([\.-]?\w+)*@\w+([\.-]?\w+)*(\.\w{2,3})+$/.test(v) ||
        "E-mail must be valid"
    ],
    select: null,
    items: ["Item 1", "Item 2", "Item 3", "Item 4"],
    checkbox: false
  }),
  methods: {
    submit() {
      if (this.$refs.form.validate()) {
        // Native form submission is not yet supported
        axios.post("/api/submit", {
          name: this.name,
          email: this.email,
          select: this.select,
          checkbox: this.checkbox
        });
      }
    },
    clear() {
      this.$refs.form.reset();
    }
  }
};
</script>
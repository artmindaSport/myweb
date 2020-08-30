<template>
  <v-container grid-list-xl>
    <v-layout row justify-center align-center wrap class="mt-4 pt-2">
      <v-flex xs12 sm12 md6 lg6 xl6>
        <h2 class="pb-4 mt-2">
          <span>{{$t('art_getIn')}}</span>
          <span class="green--text">{{$t('art_tou')}}</span>
        </h2>
        <div class="py-4 subheading font-weight-bold">
          <v-icon large color="green" left>fas fa-map-marker-alt</v-icon>
          <span>{{$t('art_site')}},&nbsp;</span>
          <span class="green--text">{{$t('art_tai')}}</span>
        </div>
        <div class="py-4 subheading font-weight-bold">
          <v-icon large color="green" left>fas fa-envelope</v-icon>
          <span>doai10007118@</span>
          <span class="green--text">gmail.com</span>
        </div>
        <div class="py-4 subheading font-weight-bold">
          <v-icon large color="green" left>fas fa-phone</v-icon>
          <span>0937&nbsp;</span>
          <span class="green--text">828 251</span>
        </div>
        <!-- <div class="py-4 subheading font-weight-bold">
          <v-icon large color="green" left>fas fa-check</v-icon>
          <span>Freelance</span>
          <span class="green--text">Available</span>
        </div> -->
      </v-flex>

      <v-flex xs12 sm12 md6 lg6 xl6>
        <h2 class="pb-4 mb-4">
          <span>{{$t('art_contact')}}</span>
          <span class="green--text">{{$t('art_form')}}</span>
        </h2>

        <form method="POST" action="https://formspree.io/xknrokpw">
          <v-text-field
            name="name"
            color="green"
            background-color="transparent"
            v-model="name"
            :error-messages="nameErrors"
            v-bind:label="$t('art_textarea_name')"
            required
            @blur="$v.name.$touch()"
          ></v-text-field>
          <v-text-field
            type="email"
            color="green"
            background-color="transparent"
            name="email"
            v-model="email"
            :error-messages="emailErrors"
            v-bind:label="$t('art_textarea_email')"
            required
            @blur="$v.email.$touch()"
          ></v-text-field>
          <v-textarea
            color="green"
            background-color="transparent"
            :counter="200"
            :error-messages="bodyErrors"
            v-model="body"
            v-bind:label="$t('art_textarea')"
            name="body"
            @blur="$v.body.$touch()"
          ></v-textarea>
          <v-btn
            @click="submit"
            type="submit"
            color="green"
            class="white--text"
            :disabled=" (body.length<=20)"
          >{{$t('art_send')}}</v-btn>
          <v-btn @click="clear">{{$t('art_clear')}}</v-btn>
        </form>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
import { validationMixin } from "vuelidate";
import {
  required,
  maxLength,
  email,
  minLength
} from "vuelidate/lib/validators";
export default {
  metaInfo: {
    title: "Contact",
    titleTemplate: "%s ← artminda's web",
    meta: [
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      {
        name: "description",
        content:
          "artminda chen's Contact please keep in Touch ContactMe"
      },
      { charset: "utf-8" },
      { property: "og:title", content: "artminda' web" },
      { property: "og:site_name", content: "artminda' web" },
      { property: "og:type", content: "website" },
      { property: "og:url", content: "https://artminda.github.io/artminda" },
      {
        property: "og:image",
        content: "https://i.imgur.com/Dcz2PGx.jpg"
      },
      {
        property: "og:description",
        content:
          "artminda chen's Contact please keep in Touch ContactMe"
      }
    ]
  },
  mixins: [validationMixin],
  validations: {
    name: { required, maxLength: maxLength(20) },
    email: { required, email },
    body: { required, minLength: minLength(20) }
  },
  data() {
    return {
      name: "",
      email: "",
      body: ""
    };
  },
  methods: {
    submit() {
      this.$v.$touch();
    },
    clear() {
      this.$v.$reset();
      this.name = "";
      this.email = "";
      this.body = "";
    }
  },
  computed: {
    nameErrors() {
      const errors = [];
      if (!this.$v.name.$dirty) return errors;
      !this.$v.name.maxLength &&
        errors.push(this.$t('art_err_name'));
      !this.$v.name.required && errors.push(this.$t('art_required_name'));
      return errors;
    },
    emailErrors() {
      const errors = [];
      if (!this.$v.email.$dirty) return errors;
      !this.$v.email.email && errors.push(this.$t('art_err_email'));
      !this.$v.email.required && errors.push(this.$t('art_required_email'));
      return errors;
    },
    bodyErrors() {
      const errors = [];
      if (!this.$v.body.$dirty) return errors;
      !this.$v.body.minLength &&
        errors.push(this.$t('art_err_body'));
      !this.$v.body.required && errors.push(this.$t('art_required_body'));
      return errors;
    }
  }
};
</script>

<style lang="scss" scoped>
</style>

<template>
  <div class="TheMenu">
    <v-layout row justify-center align-center wrap class="mt-4 pt-2">
      <v-flex xs12 md6 lg6 >
         <v-toolbar-items class="">
        <v-btn flat to="/" active-class="green--text headline">{{$t('art_home')}}</v-btn>
        <v-btn flat to="/resume" active-class="green--text headline">{{$t('art_re')}}</v-btn>
        <v-btn flat to="/services" active-class="green--text headline">{{$t('art_ser')}}</v-btn>
        <v-btn flat to="/portfolio" active-class="green--text headline">{{$t('art_por')}}</v-btn>
        <v-btn flat to="/blog" active-class="green--text headline">{{$t('art_blog')}}</v-btn>
        <v-btn flat to="/contact" active-class="green--text headline">{{$t('art_con')}}</v-btn>
        <v-select
          v-model="selectLang"
          class="selectWidth ml-3 mr-3"
          :items="items"
          label="select lang"
          dense
          single-line
        ></v-select>
        <v-btn @click="changeTheme" depressed small icon>
          <v-icon v-if="goDark==true">fas fa-sun</v-icon>
          <v-icon v-else>fas fa-moon</v-icon>
        </v-btn>
      </v-toolbar-items>
      <v-container>
        <div class="infoArea">
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
        </div>
       </v-container> 
      </v-flex>
      <v-flex xs12 md6 >
      <v-container>
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
        </v-container>
      </v-flex>
    </v-layout>
  </div>
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
      body: "",
      selectLang: localStorage.getItem('lang') === "tw" ? "中文" : "English" ,
      items:["English","中文"],
      drawer: null
    };
  },
  watch:{
    selectLang(val){
      this.$emit("changeLang", val);
    }
  },
  methods: {
    changeTheme() {
      this.$emit("changeTheme", this.goDark);
    },
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
  .TheMenu {
    width: 100%;
    position: absolute;
    z-index: 888;
    background-color: #ffa7a7;
    top: 0;
    bottom: 0;
    // opacity: 50%;
  }
</style>

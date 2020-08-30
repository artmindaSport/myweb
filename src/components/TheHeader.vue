<template>
  <div>
    <v-navigation-drawer v-model="drawer" absolute temporary app width="150" height="380">
      <v-list class="pt-4">
        <v-list-tile active-class="green--text" to="/">
          <v-list-tile-content>
            <v-list-tile-title>{{$t('art_home')}}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile active-class="green--text" to="/resume">
          <v-list-tile-content>
            <v-list-tile-title>{{$t('art_re')}}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile active-class="green--text" to="/services">
          <v-list-tile-content>
            <v-list-tile-title>{{$t('art_ser')}}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile active-class="green--text" to="/portfolio">
          <v-list-tile-content>
            <v-list-tile-title>{{$t('art_por')}}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile active-class="green--text" to="/blog">
          <v-list-tile-content>
            <v-list-tile-title>{{$t('art_blog')}}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile active-class="green--text" to="/contact">
          <v-list-tile-content>
            <v-list-tile-title>{{$t('art_con')}}</v-list-tile-title>
          </v-list-tile-content>
        </v-list-tile>
        <v-list-tile>
            <v-flex class="xs10">
             <v-select
              v-model="selectLang" 
              class="hidden-md-and-up"
              :items="items"
              label="select"
              dense
              single-line
              ></v-select>
            </v-flex> 
        </v-list-tile>  
      </v-list>
    </v-navigation-drawer>
    <v-toolbar flat dense color="transparent" scroll-off-screen>
      <v-toolbar-side-icon class="hidden-md-and-up" @click.stop="drawer = !drawer"></v-toolbar-side-icon>
      <v-toolbar-title class="headline">
        <span class="font-weight-light">artminda</span>
        <span class="green--text">Chen</span>
      </v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn @click="changeTheme" depressed small icon class="hidden-md-and-up">
        <v-icon v-if="goDark==true">fas fa-sun</v-icon>
        <v-icon v-else>fas fa-moon</v-icon>
      </v-btn>
    <!-- pc -->
      <v-toolbar-items class="hidden-sm-and-down">
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
    </v-toolbar>
  </div>
</template>

<script>
export default {
  props: {
    goDark: {
      type: Boolean
    },
    lang: {
      type: String
    }
  },
  data() {
    return {
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
    }
  }
};
</script>

<style >
.selectWidth {
  width: 109px;
  -webkit-box-align: center;
  -ms-flex-align: center;
  align-items: center;
  -ms-flex-item-align: center;
  align-self: center;
}
</style>
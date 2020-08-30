<template>
  <v-app :dark="goDark">
    <v-content>
      <div>
        <hamburger :goDark="goDark" :lang="lang" @menu="showMenu($event)" @changeTheme="updateTheme($event)" @changeLang="updateLang($event)" />
        <!-- <TheHeader :goDark="goDark" :lang="lang" @changeTheme="updateTheme($event)" @changeLang="updateLang($event)"/> -->
        <!-- <TheTips v-if="$route.name === 'home'"/> --> 
         <transition
          name="router-animation"
          mode="out-in"
          enter-active-class="animated fadeInRight fast"
          leave-active-class="animated fadeOutRight faster"
        > 
        <TheMenu v-if="menu" :goDark="goDark" :lang="lang" @changeTheme="updateTheme($event)" @changeLang="updateLang($event)"/>
        </transition>
        <div class="screenHight">     
        <transition
          name="router-animation"
          mode="out-in"
          enter-active-class="animated bounceInDown fast"
          leave-active-class="animated bounceOutDown faster"
        > 
          <router-view></router-view>
        </transition>
        <!-- <TheFooter/> -->
        </div>
      </div>
    </v-content>
  </v-app>
</template>

<script>
import TheMenu from "./components/TheMenu";
import hamburger from "./components/hamburger";
import TheTips from "./components/TheTips";
import TheHeader from "./components/TheHeader";
import TheFooter from "./components/TheFooter";
import i18n from 'i18n'

export default {
  name: "App",
  metaInfo: {
    title: "Home",
    titleTemplate: "%s ← artminda's web",
    meta: [
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      { name: "description", content: "artminda chen's Portfolio" },
      { charset: "utf-8" },
      { property: "og:title", content: "artminda' web" },
      { property: "og:site_name", content: "artminda' web" },
      { property: "og:type", content: "website" },
      { property: "og:url", content: "https://artminda.web" },
      {
        property: "og:image",
        content: "https://i.imgur.com/Dcz2PGx.jpg"
      },
      { property: "og:description", content: "artminda chen's Portfolio" }
    ]
  },
  components: {
    hamburger,
    TheHeader,
    TheFooter,
    TheTips,
    TheMenu
  },
  data() {
    return {
      menu: false, 
      goDark: false, 
      lang: "en"  
    };
  },
  methods: {
    showMenu(val){
      this.menu = val
      console.log("showMenu:",this.menu)
    },
    updateTheme(updatedTheme) {
      this.goDark = !updatedTheme;
    },
    updateLang(newLang){
      console.log("APP-newLang-EMIT:", typeof newLang, newLang)
      if (newLang === "中文"){
        this.$i18n.locale = "tw"
        localStorage.setItem("lang", "tw")
        return
      }
      this.$i18n.locale = newLang
      localStorage.setItem("lang", newLang)
    }
  },
  mounted(){
    console.log("APP-menu:", this.menu) 
  }
};
</script>
<style>
@import "https://cdnjs.cloudflare.com/ajax/libs/animate.css/3.7.0/animate.min.css";

* {
  font-family:'Microsoft JhengHei',sans-serif;  
}

::-webkit-scrollbar {
width: 5px;
}
::-webkit-scrollbar-track {
-webkit-border-radius: 10px;
border-radius: 10px;
margin:80px 0 5px 0;
}
::-webkit-scrollbar-thumb {
-webkit-border-radius: 4px;
border-radius: 4px;
background: rgb(219,219,219);
}

.screenHight {
  overflow: scroll;
  overflow-x: hidden;
  height: 100vh;
  padding: 2rem;
  border: 10px red solid;
}

pre {
    font-size: 1rem;
    padding: 20px;
    border-radius: 5px;
    border: 1px solid #282c34;
    background: #282c34;
    color: #DCDCDC;
    display: block;
    font-family: monospace;
    white-space: pre;
    margin: 1em 0px;
 }

code {
  background: #282c34;
  display: block;
  overflow-x: auto;
  padding: 0.5em;
  color: #DCDCDC;
}

</style>

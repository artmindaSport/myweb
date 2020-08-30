<template>
  <v-container grid-list-xl>
    <h2 class="pl-4">
      <span>Web</span>
      <span class="green--text">Portfolio</span>
    </h2>
    <v-layout row justify-center align-center wrap class="mt-4 pt-2">
      <v-dialog
        v-model="project.dialog"
        lazy
        max-width="1000"
        v-for="project in projects"
        :key="project.title"
      >
        <template v-slot:activator="{ on }">
          <v-flex xs12 sm6 md4 lg4 xl4 v-on="on">
            <v-card hover flat color="transparent">
              <v-img
                :src="project.poster"
                :alt="project.title"
                height="230"
                lazy-src="https://cdn.dribbble.com/users/503653/screenshots/3143656/fluid-loader.gif"
              ></v-img>
              <v-card-title primary-title class="justify-center">{{project.title}}</v-card-title>
            </v-card>
          </v-flex>
        </template>
        <v-card v-if="project.dialog">
          <v-img :src="project.poster"></v-img>
          <v-card-text>
            <h3 class="headline mb-0">
              <span>Technology</span>
            </h3>
            <span v-for="techitem in project.tech" :key="techitem">
              <v-chip color="green" text-color="white">{{techitem}}</v-chip>
            </span>
          </v-card-text>
          <v-card-actions>
            <v-btn v-if="project.git" flat large dark color="green" :href="project.git" target="_blank">
              <v-icon left>fab fa-github</v-icon>GitHub
            </v-btn>
            <v-btn large flat dark color="green" :href="project.demo" target="_blank">
              <v-icon left>fas fa-desktop</v-icon>Demo
              <span v-if="project.title == 'yabo_mobile_practice'" class="ml-1">
                ( vpn need China )
              </span>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  metaInfo: {
    title: "Web Portfolio",
    titleTemplate: "%s ← artminda's web",
    meta: [
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      {
        name: "description",
        content:
          "artminda chen's Web Portfolio Vue Vue.js Nuxt Nuxt.js HTML CSS Vuetify Axios GraphQL JavaScript Web Developer Front-End Frontend Designer App Responsive"
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
          "artminda chen's Web Portfolio Vue Vue.js Nuxt Nuxt.js HTML CSS Vuetify Axios GraphQL JavaScript Web Developer Front-End Frontend Designer App Responsive"
      }
    ]
  },
  data() {
    return {
      dialog: false,
      projects: [
         {
          dialog: false,
          title: "yabo_mobile_practice (vpn: China)",
          demo: "https://xj-mbs-yabo.prdasbbwla1.com/m/en-gb/",
          tech: {
            tech1: "vue-cli",
            tech2: "webpack config",
            tech3: "RESTful API",
            tech4: "javascript ES6",
            tech5: "Route",
            tech6: "vuex",
            tech7: "element ui",
            tech8: "SASS"
          },
          poster: "https://i.imgur.com/nkUJLrm.jpg",
        },
        {
          dialog: false,
          title: "This Site",
          git: "https://github.com/artminda/artminda",
          demo: "https://artminda.github.io/artminda",
          tech: {
            tech1: "vue-cli",
            tech2: "JavaScript",
            tech3: "vuetify",
            tech4: "storyblok"
          },
          poster: "https://i.imgur.com/7MxhQDD.jpg",
        },
        {
          dialog: false,
          title: "Portfolio_basic",
          git: "https://github.com/artminda/Portfolio_basic",
          demo: "https://artminda.github.io/Portfolio_basic",
          tech: {
            tech1: "vue-cli",
            tech2: "JavaScript",
            tech3: "vuetify",
            tech4: "storyblok API",
            tech5: "i18n",
            tech6: "lottie"
          },
          poster: "https://i.imgur.com/bY1oT8G.jpg",
        },
        {
          dialog: false,
          title: "creat_fun",
          git: "https://github.com/artminda/creatFun",
          demo: "https://artminda.github.io/creatFun",
          tech: {
            tech1: "ui design",
            tech2: "css",
            tech3: "html",
            tech4: "JQery"
          },
          poster: "https://i.imgur.com/TO4wz9M.jpg",
        },
        {
          dialog: false,
          title: "My Old Web Portfolio",
          git: "https://github.com/artminda/artminda-old",
          demo: "https://artminda.github.io/artminda-old",
          tech: {
            tech1: "ui design",
            tech2: "bootstrap",
          },
          poster: "https://i.imgur.com/5KnIrGS.jpg",
        }, 
        {
          dialog: false,
          title: "oasis bitcoin",
          git: "https://github.com/artminda/oasis",
          demo: "http://oasis.byethost9.com/index.php",
          tech: {
            tech1: "ui design",
            tech2: "bootstrap",
            tech3: "php",
          },
          poster: "https://i.imgur.com/Tm5cS5K.jpg",
        },
        {
          dialog: false,
          title: "Admin dashboard",
          git: "https://github.com/artminda/artminda-management",
          demo: "https://artminda.github.io/artminda-management/",
          tech: [
             "vue cli",
             "JavaScript",
             "sass",
             "element ui",
             "proxy api"
          ],
          poster: "https://i.imgur.com/0kctvSn.jpg"
        },
        // {
        //   dialog: false,
        //   title: "GraphQL practice",
        //   git: "https://github.com/EldinZaimovic/SnowBall-Project",
        //   demo: "https://artminda.github.io/GraphQL-practice/index.html",
        //   tech: {
        //     tech1: "VUE",
        //     tech2: "GraphQL",
        //     tech3: "Axios",
        //     tech4: "JavaScript"
        //   },
        //   poster: "https://i.imgur.com/rXHBs36.png"
        // },
        {
          dialog: false,
          title: "Lodash practice",
          git: "https://github.com/artminda/Lodash-practice",
          demo: "https://artminda.github.io/Lodash-practice/index.html",
          tech: {
            tech1: "VUE",
            tech2: "Lodash",
            tech3: "HTML",
            tech4: "JavaScript"
          },
          poster: "https://i.imgur.com/kCN1CFH.png"
        },
        {
          dialog: false,
          title: "poople",
          git: "https://github.com/artminda/poople",
          demo: "https://artminda.github.io/poople/",
          tech: {
            tech1: "bootstrp",
            tech2: "RWD",
            tech3: "HTML"
          },
          poster: "https://i.imgur.com/VDE7Bdp.jpg"
        },
      ]
    };
  }
};
</script>

<style  scoped>
</style>
<template>
  <v-container grid-list-xl>
    <h2 class="pl-4">
      <span>Video</span>
      <span class="green--text">Portfolio</span>
    </h2>
    <v-layout row justify-center align-center wrap class="mt-4 pt-2">
      <v-dialog
        v-model="video.dialog"
        lazy
        max-width="800"
        v-for="video in videos"
        :key="video.title"
      >
        <template v-slot:activator="{ on }">
          <v-flex xs12 sm6 md4 lg4 xl4 v-on="on">
            <v-card hover flat color="transparent">
              <v-img
                :src="video.poster"
                aspect-ratio="1.7778"
                :alt="video.title"
                lazy-src="https://cdn.dribbble.com/users/503653/screenshots/3143656/fluid-loader.gif"
                contain
              ></v-img>
              <v-card-title primary-title class="justify-center">{{video.title}}</v-card-title>
            </v-card>
          </v-flex>
        </template>
        <v-card v-if="video.dialog">
          <plyr>
            <div class="plyr__video-embed">
              <iframe :src="video.href" allowfullscreen allowtransparency allow="autoplay"></iframe>
            </div>
          </plyr>
        </v-card>
      </v-dialog>
    </v-layout>
  </v-container>
</template>

<script>
import { PlyrVideo } from "vue-plyr";

export default {
  metaInfo: {
    title: "Video Portfolio",
    titleTemplate: "%s ← artminda's web",
    meta: [
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      {
        name: "description",
        content:
          "artminda chen's Services Adobe Premire After Effects Video Ad's Social Media Logo Animation Instagram Facebook Video Editing Advetising"
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
          "artminda chen's Services Adobe Premire After Effects Video Ad's Social Media Logo Animation Instagram Facebook Video Editing Advetising"
      }
    ]
  },
  components: { plyr: PlyrVideo },
  data() {
    return {
      dialog: false,
      videos: [
        {
          dialog: false,
          title: "text title adv",
          href: "https://www.youtube.com/embed/xC9j8sDYhgQ",
          type: "text/html",
          youtube: "xC9j8sDYhgQ",
          poster: "https://i.imgur.com/TvCZjc4.jpg"
        },
        {
          dialog: false,
          title: "text title adv",
          href: "https://www.youtube.com/embed/50oe_7CfIQw",
          type: "text/html",
          youtube: "50oe_7CfIQw",
          poster: "https://i.imgur.com/TUFVcVe.jpg"
        },
        {
          dialog: false,
          title: "short movie practice",
          href: "https://www.youtube.com/embed/6z5StwkL-BY",
          type: "text/html",
          youtube: "6z5StwkL-BY",
          poster: "https://i.imgur.com/XFtEDbA.jpg"
        },
        {
          dialog: false,
          title: "short horror movie practice",
          href: "https://www.youtube.com/embed/3jL7d4nuv_E",
          type: "text/html",
          youtube: "3jL7d4nuv_E",
          poster: "https://i.imgur.com/Pi52KIA.jpg"
        },
        {
          dialog: false,
          title: "short practice",
          href: "https://www.youtube.com/embed/3BhEqdZhScE",
          type: "text/html",
          youtube: "3BhEqdZhScE",
          poster: "https://i.imgur.com/KPjCy7e.jpg"
        },
        {
          dialog: false,
          title: "short adv practice",
          href: "https://www.youtube.com/embed/g67wKWBWR38",
          type: "text/html",
          youtube: "g67wKWBWR38",
          poster: "https://i.imgur.com/IiZ7Rxb.jpg"
        }
      ]
    };
  }
};
</script>

<style  scoped>
@import "../../../node_modules/vue-plyr/dist/vue-plyr.css";
</style>
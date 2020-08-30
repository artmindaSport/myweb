<template>
  <v-container grid-list-xl>
    <v-layout row justify-center align-center wrap class="mt-4 pt-2">
      <v-flex xs12 sm12 md12 lg12 xl12>
        <h2 class="pl-4">
          <span>My</span>
          <span class="green--text">Services</span>
        </h2>
      </v-flex>
      <v-flex v-for="service in services" :key="service.src" xs6 sm3 md3 lg3 xl3>
        <v-card  flat color="transparent" :style="{'cursor':'context-menu'}">
          <v-card-title></v-card-title>
          <v-img
            :src="service.src"
            height="100"
            aspect-ratio="2.75"
            :alt="'artminda do '+service.title"
            lazy-src="https://cdn.dribbble.com/users/503653/screenshots/3143656/fluid-loader.gif"
            contain
          ></v-img>
          <v-card-title class="justify-center">
            <v-flex text-xs-center subheading font-weight-bold>{{service.title}}</v-flex>
          </v-card-title>
        </v-card>
      </v-flex>
      <v-flex xs12 sm12 md12 lg12 xl12>
        <h2 class="pl-4">
          <span>My</span>
          <span class="green--text">Clients</span>
        </h2>
      </v-flex>

      <v-flex v-for="client in clients" :key="client.name" xs6 sm4 md3 lg2 xl2>
        <v-card flat :href="client.href" target="_blank" color="transparent">
          <v-hover>
            <v-img
              slot-scope="{ hover }"
              :src="client.src"
              :alt="client.name+' logo'"
              lazy-src="https://cdn.dribbble.com/users/503653/screenshots/3143656/fluid-loader.gif"
              height="100"
              width="160"
              aspect-ratio="2.75"
              contain
            >
              <v-expand-transition>
                <div
                  v-if="hover"
                  class="transition-fast-in-fast-out teal green lighten-3 v-img--reveal"
                  style="height: 100%;"
                ></div>
              </v-expand-transition>
            </v-img>
          </v-hover>
        </v-card>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  metaInfo: {
    title: "Services",
    titleTemplate: "%s ← artminda's web",
    meta: [
      { name: "viewport", content: "width=device-width, initial-scale=1" },
      {
        name: "description",
        content:
          "artminda chen's Services Web Development Video Editing Graphic Design Front-End Advetising"
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
          "artminda chen's Services Web Development Video Editing Graphic Design Front-End Advetising"
      }
    ]
  },
  data() {
    return {
      clients: [
       {
        name: "元美電器",
        src: "https://i.imgur.com/37J0C1y.png",
        href: "https://www.facebook.com/am2213113/"
        },
       {
        name: "怡安藥局",
        src: "https://i.imgur.com/EzYZ15g.png",
        href: "https://www.facebook.com/pages/%E6%80%A1%E5%AE%89%E8%97%A5%E5%B1%80/157407534395817"
        },
        {
        name: "大林濕地保育協會",
        src: "https://i.imgur.com/YmiYD93.png",
        href: ""
        },
        {
        name: "taxi",
        src: "https://i.imgur.com/XBCrKaw.png",
        href: ""
       },
        {
        name: "spa",
        src: "https://i.imgur.com/WTzttHV.png",
        href: ""
        }
      ],
      services: [
        {
          src: "https://i.imgur.com/GvTt5GG.png",
          title: "Web Development"
        },
        {
          src: "https://i.imgur.com/g74mGuU.png",
          title: "Web Design"
        },
         {
          src: "https://i.imgur.com/bgSxyzI.jpg",
          title: "Package Design"
        },
        {
          src: "https://i.imgur.com/wXLtLKy.png",
          title: "Video Editing"
        }
      ]
    };
  }
};
</script>
<style >
.v-img--reveal {
  opacity: 0.3;
}
</style>
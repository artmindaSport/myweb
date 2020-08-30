<template>
  <v-layout column justify-center class="mt-4 pt-2" v-editable="result">
    <h1 class="text-xs-center mb-4 pb-2">{{result.title}}</h1>
    <span v-if="result && result.date">{{result.date}}</span>
    <v-img :src="result.image" aspect-ratio="2.75" height="330" contain :alt="result.title"></v-img>
    <v-layout column justify-center align-center class="mt-4 pt-2">
      <p v-html="body"></p>
    </v-layout>
    <br>
    <br>
    <v-btn large flat to="/blog" class="green--text">
      <v-icon>arrow_back</v-icon>Back to Blog
    </v-btn>
  </v-layout>
</template>

<script>
import marked from "marked";
import StoryblokClient from "storyblok-js-client";
const token = "mUT1Vr0FJ9aOLrdlHaMSbQtt";
let storyapi = new StoryblokClient({
  accessToken: token
});

export default {
  data() {
    return {
      posts: [],
      result: {}
    };
  },
  metaInfo() {
    return {
      title: this.result.title,
      titleTemplate: "%s ← artminda's Blog",
      meta: [
        { name: "viewport", content: "width=device-width, initial-scale=1" },
        {
          name: "description",
          content: this.result.content
        },
        { charset: "utf-8" },
        { property: "og:title", content: "artminda' web" },
        { property: "og:site_name", content: "artminda' web" },
        { property: "og:type", content: "website" },
        { property: "og:url", content: "https://artminda.github.io/artminda/" },
        {
          property: "og:image",
          content: "https://i.imgur.com/Dcz2PGx.jpg"
        },
        {
          property: "og:description",
          content: this.result.content
        }
      ]
    };
  },
  computed: {
    body() {
      if (this.result.content){
        return marked(this.result.content);
      }
        return ''
    }
  },

  created() {
    window.storyblok.init({
      accessToken: token
    });
    window.storyblok.on("change", () => {
      this.getStory("article", "draft");
    });
    window.storyblok.pingEditor(() => {
      if (window.storyblok.isInEditor()) {
        this.getStory("article", "draft");
      } else {
        this.getStory("article", "published");
      }
    });
  },

  methods: {
    getStory(version) {
      storyapi
        .get("cdn/stories", {
          version: "draft",
          starts_with: "article/"
        })
        .then(res => {
          this.posts = res.data.stories.map(bp => {
            return {
              id: bp.slug,
              title: bp.content.title,
              blok: bp.content,
              image: bp.content.teaser_image,
              content: bp.content.long_text,
              date: bp.content.date
            };
          });
          console.log('this.posts:',this.posts)
          this.result = this.posts.find(
            rightPost => rightPost.id === this.$route.params.id
          );
          console.log('this.result:',this.result)
        })
        .catch(error => {
          console.log(error);
        });
    }
  }
};
</script>

<style scoped>
</style>
<template>
  <div class="home">
    <a
      href="https://accounts.spotify.com/authorize?client_id=5b392530b00147d788370b060832b220&response_type=code&redirect_uri=http://localhost:8080"
    >
      Connect to Spotify
    </a>
    <h1>{{ message }}</h1>

    <div v-for="post in redditPosts">
      <h2>{{ post.data.title }}</h2>
      <p>{{ post.data.url }}</p>
    </div>

    <div v-for="post in posts">
      <h2>{{ post.title }}</h2>
      <p>{{ post.body }}</p>
    </div>
  </div>
</template>

<style></style>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      message: "Welcome to Vue.js!",
      posts: [],
      redditPosts: []
    };
  },
  created: function() {
    axios.get("https://jsonplaceholder.typicode.com/posts").then(response => {
      console.log(response.data);
      this.posts = response.data;
    });
    axios.get("http://localhost:3000/api/reddit_programming").then(response => {
      console.log(response.data);
      this.redditPosts = response.data.data.children;
    });
    axios.get("http://localhost:3000/api/newsapi_headlines").then(response => {
      console.log("newsapi", response.data);
    });
  },
  methods: {}
};
</script>

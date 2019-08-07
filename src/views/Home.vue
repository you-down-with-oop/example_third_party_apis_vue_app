<template>
  <div class="home">
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

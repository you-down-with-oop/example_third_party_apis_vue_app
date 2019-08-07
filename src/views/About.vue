<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div v-for="artist in artists">
      <h2>{{ artist.name }}</h2>
      <div v-for="image in artist.images">
        <img v-bind:src="image.url" alt="" />
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function() {
    return {
      artists: []
    };
  },
  created: function() {
    var spotifyAccessToken = localStorage.getItem("spotify_access_token");
    if (spotifyAccessToken) {
      axios
        .get("http://localhost:3000/api/spotify_search?spotify_access_token=" + spotifyAccessToken)
        .then(response => {
          console.log(response.data.artists.items);
          this.artists = response.data.artists.items;
        });
    }
  }
};
</script>

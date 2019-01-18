<template lang="pug">
  #app
    img(alt="Vue logo" src="./assets/logo.png")
    h1 PlatziMusic
    select(v-model="selectedCountry")
      option(v-for="country in countries" :value="country.value") {{ country.name }}
    Spinner(v-show="loading")
    ul
      Artist(v-for="artist in artists" :artist="artist" :key="artist.mbid")
</template>

<script>
import Artist from "./components/Artist.vue";
import Spinner from "./components/Spinner";
import getArtists from "./api";

export default {
  name: "app",
  data() {
    return {
      artists: [],
      countries: [
        { name: "Republica Dominicana", value: "dominican republic" },
        { name: "Colombia", value: "colombia" },
        { name: "Argentina", value: "argentina" },
        { name: "España", value: "spain" }
      ],
      selectedCountry: "dominican republic",
      loading: true
    };
  },
  components: {
    Artist,
    Spinner
  },
  methods: {
    refreshArtists() {
      this.loading = true;
      this.artists = [];
      getArtists(this.selectedCountry).then(artists => {
        this.loading = false;
        this.artists = artists;
      });
    }
  },
  mounted() {
    this.refreshArtists();
  },
  watch: {
    selectedCountry: function() {
      this.refreshArtists();
    }
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>

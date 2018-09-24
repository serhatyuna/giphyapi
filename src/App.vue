<template>
  <div id="app">
    <search @SearchRequested="handleSearch"></search>
    <p v-if="isLoading">Loading...</p>
    <h1 v-if="!isLoading && !gifs.length">Nothing found!</h1>
    <h1 v-if="!isLoading && searchedQuery && gifs.length > 0">Results for: "{{ searchedQuery }}"</h1>
    <preview :gifs=gifs></preview>
  </div>
</template>

<script>
import Search from "./components/Search.vue";
import Preview from "./components/Preview.vue";

export default {
  name: "app",
  components: { Search, Preview },
  data() {
    return {
      isLoading: true,
      gifs: [],
      searchedQuery: "",
      apiKey: ""
    };
  },
  methods: {
    doQuery(url) {
      fetch(url)
        .then(res => {
          return res.json();
        })
        .then(res => {
          res.data.forEach(element => {
            element.images.fixed_height.url = element.images.fixed_height.url.replace(
              /media[0-9]/g,
              "i"
            );
          });
          this.gifs = res.data;
          this.isLoading = false;
        });
    },
    handleSearch(query) {
      this.gifs = [];
      this.isLoading = true;
      const url = `http://api.giphy.com/v1/gifs/search?q=${query}&api_key=${
        this.apiKey
      }`;
      this.doQuery(url);
      this.searchedQuery = query;
    }
  },
  created() {
    const url = `http://api.giphy.com/v1/gifs/trending?api_key=${this.apiKey}`;
    this.doQuery(url);
  }
};
</script>

<style>
body {
  margin: 0;
}

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

p {
  margin-top: 50px;
}
</style>

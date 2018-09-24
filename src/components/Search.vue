<template>
  <div class="search">
    <input type="text" @keypress.enter="handleSearch" v-model="query" autofocus>
    <button @click="handleSearch">Search</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      query: ""
    };
  },
  methods: {
    handleSearch() {
      this.query = this.query.trim();
      if (this.query) {
        this.$emit("SearchRequested", this.query);
      }
    }
  }
};
</script>

<style>
.search {
  position: relative;
  overflow: hidden;
  width: 421px;
  margin: 40px 0 0 40px;
}

.search input {
  box-sizing: border-box;
  padding: 10px 100px 10px 20px;
  border: 1px solid #eee;
  border-radius: 5px;
  width: 420px;
  font-size: 1em;
  transition: border-color 150ms;
}

.search button {
  padding: 10px 15px;
  border: 1px solid #376ea5;
  background: #4183c4;
  color: #fff;
  cursor: pointer;
  font-size: 1em;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  border-top-left-radius: 0;
  border-bottom-left-radius: 0;
  opacity: 0.8;
  transition: opacity 150ms;
  position: absolute;
  right: 0;
  top: 0;
}

.search input:hover {
  border-color: #ddd;
}

.search button:focus,
.search input:focus {
  outline: 0;
}

.search input:focus {
  border-color: #ccc;
}

.search button:focus {
  background: #376ea5;
}

.search button:hover {
  opacity: 1;
}
</style>

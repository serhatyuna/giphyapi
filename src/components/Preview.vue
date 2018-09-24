<template>
  <div>
    <ul>
      <li v-for="(gif, index) in gifs" :key="gif.id">
        <img :src="gif.images.fixed_height.url">
        <div>
          <button class="imgButton copyButton" @click="copyUrl(gif.images.fixed_height.url, index)">
            <span v-show="currentlyCopiedIndex !== index">Copy URL</span>
            <span v-show="currentlyCopiedIndex === index" class="greenColor">Copied!</span>
          </button>
          <button class="imgButton downloadButton">
            <a :href="gif.images.fixed_height.url">Download</a>
          </button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import Vue from "vue";
import VueClipboard from "vue-clipboard2";
Vue.use(VueClipboard);

export default {
  props: ["gifs"],
  data() {
    return {
      currentlyCopiedIndex: ""
    };
  },
  methods: {
    copyUrl(url, index) {
      let self = this; // to save 'this' inside of 'then'
      this.$copyText(url).then(() => {
        self.currentlyCopiedIndex = index;
        setTimeout(() => {
          self.currentlyCopiedIndex = "";
        }, 1500);
      });
    }
  }
};
</script>

<style scoped>
ul {
  margin-top: 50px;
  display: flex;
  justify-content: space-around;
  flex-flow: row wrap;
  padding: 0 20px;
}

li {
  list-style: none;
  margin-bottom: 60px;
  position: relative;
}

:focus {
  outline: 0;
}

li div {
  display: flex;
  margin-top: -4px;
}

img {
  max-height: 200px;
}

.imgButton {
  width: 50%;
  height: 40px;
  box-sizing: border-box;
  cursor: pointer;
  padding: 10px 0;
  background: #fff;
  color: #777;
  border: 1px solid #eee;
  transition: background-color, border-color 200ms;
}

.imgButton:hover {
  background-color: #eee;
  border-color: #ccc;
}

a {
  text-decoration: none;
  color: #777;
}

a:visited {
  color: #777;
}

.greenColor {
  color: #29b90e;
}
</style>

<script setup lang="ts">

import {ref, watch} from "vue";
import axios from "axios";

const text = ref('');

const url = ref('https://cataas.com/cat');


const catImg = async () => {
  const {data} = await axios('https://cataas.com/cat', {
    responseType: "arraybuffer",
  });
  const blob = new Blob([data], {type: "image/png"});
  url.value = URL.createObjectURL(blob);
}

const catGif = async () => {
  const {data} = await axios('https://cataas.com/cat/gif', {
    responseType: "arraybuffer",
  });
  const blob = new Blob([data], {type: "image/gif"});
  url.value = URL.createObjectURL(blob);
}

const catText = async () => {
  const req = 'https://cataas.com/cat/says/' + text.value;
  const {data} = await axios(req, {
    responseType: "arraybuffer",
  });
  const blob = new Blob([data], {type: "image/png"});
  url.value = URL.createObjectURL(blob);
}



</script>

<template>
  <div class="main">
      <div class="menu">
        <button type="submit" @click="catImg()">Cat image</button>
        <button type="submit" @click="catGif()">Cat gif</button>
        <div class="saying">
          <button type="submit" @click="catText()">Cat's saying</button>
          <input placeholder="text" v-model="text"/>
        </div>
      </div>
      <img :ref="url" :src="url"/>
  </div>
</template>

<style scoped>
.main {
  display: flex;
  justify-content: space-between;
  width: 800px;
}

.menu {
  display: flex;
  flex-direction: column;
  padding: 5px;
}

button {
  width: 200px;
  height: 50px;
  margin: 5px;
  border-radius: 5px;
  border: 0;
  cursor: pointer;
  background: #c5c5c5;
}

input {
  width: 200px;
  height: 50px;
  margin: 5px;
  border-radius: 5px;
  text-align: center;
}

.saying {
  display: flex;
  flex-direction: row;
}

button:hover {
  background: gray;
}

img {
  width: 400px;
  height: 400px;
}

</style>

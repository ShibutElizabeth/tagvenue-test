<template>
  <div>New URL (https only)</div>
  <input type=text v-model="url1" :class="{error: isInvalidUrl(url1)}" />
  <br><br>
  <div>Confirm URL</div>
  <input type=text v-model="url2" :class="{error: isInvalidUrl(url2)}" />
  
  <div class="errors">
      <div class="error-text" v-show="url1 != url2">
        Provided URLs must be the same!
      </div>

      <div class="error-text" v-show="url1 != url2">
        Provided URL must be a valid https link!
      </div>
  </div>
  <br>
  <button @click="submit">Save</button>

</template>

<script>
import HelloWorldVue from "./components/HelloWorld.vue";
import { addNewUrl } from "./api";
export default {
  name: "App",
  data() {
    return {
      url1: '',
      url2: null,
      notSame: null,
    };
  },
  watch: {
  },
  components: {
    HelloWorld: HelloWorldVue,
  },
  methods: {
    isInvalidUrl(url) {
      return !url || !url.match(/https:\/\/.*/)?.[0];
    },
    submit() {
      // clean whitespace from start/end
      var clean = this.url1.replaceAll(' ', '');

      addNewUrl(clean).then(function () {
        alert('Saved!');
      });
    },
  },
};
</script>

<style>
:root {
  --brand-danger: #ff0000;
}

input {
  outline: none; /* Prevent blue border when error border is visible */
}

.error-text {
  padding: 16px;
  color: --brand-danger;
  margin-bottom: -16px;
}

.error {
  border: 1px solid red;
}
</style>

<template>
  <div>
    <h1>Repos</h1>
    <div v></div>
  </div>
</template>

<script>
import Issues from "./repo/Issues.vue";
import { octokitMixin } from "./../mixins/octokitMixin";

export default {
  name: "Repos",
  components: {
    Issues,
  },
  // DATA
  data() {
    return {
      repos: [],
    };
  },
};
</script>

<style>
</style>
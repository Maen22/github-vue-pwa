<template>
  <form @submit.prevent="saveToken">
    <div>
      <label for="githubToken">Github Token</label>
      <br />
      <input type="text" id="githubToken" v-model="githubToken" />
    </div>
    <div>
      <input type="submit" value="Save token" />
      <button type="button" @click="clearToken">Clear token</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "GitHubTokenForm",
  // DATA
  data() {
    return {
      githubToken: "",
    };
  },
  // BEFOR MOUNT ==> To git token if there is one
  beforeMount() {
    this.githubToken = localStorage.getItem("github-token");
  },
  // METHODS
  methods: {
    saveToken() {
      localStorage.setItem("github-token", this.githubToken);
    },
    clearToken() {
      localStorage.clear();
    },
  },
};
</script>

<style>
</style>
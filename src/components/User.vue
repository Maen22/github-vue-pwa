<template>
  <div>
    <h1>User Info</h1>
    <ul>
      <li>
        <img :src="userData.avatar_url" id="avatar" />
      </li>
      <li>username: {{ userData.login }}</li>
      <li>followers: {{ userData.followers }}</li>
      <li>plan: {{ userData.pla && userData.plan.name }}</li>
    </ul>
  </div>
</template>

<script>
import { octokitMixin } from "./../mixins/octokitMixin";

export default {
  name: "User",
  // DATA
  data() {
    return {
      userData: {},
    };
  },
  // MIXINS
  mixins: [octokitMixin],
  async mounted() {
    const octokit = this.createOctokitClient();
    const { data: userData } = await octokit.request("/user");
    this.userData = userData;
  },
  // METHODS
  methods: {
    saveToken() {},
  },
};
</script>

<style scoped>
#avatar {
  width: 50px;
  height: 50px;
}
</style>
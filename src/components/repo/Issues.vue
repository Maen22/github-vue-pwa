<template>
  <div v-if="issues.length > 0">
    <button @click="showIssues = !showIssues">
      {{ showIssues ? "Hide" : "Show" }} issues
    </button>
    <div v-if="showIssues">
      <div v-for="i in issues" :key="i.id">
        <h3>{{ i.title }}</h3>
        <a :href="i.url">Go to issue</a>
        <IssueComments :owner="owner" :repo="repo" :issueNumber="i.number" />
      </div>
    </div>
  </div>
</template>

<script>
import { octokitMixin } from "../../mixins/octokitMixin";
import IssueComments from "./issue/Comments.vue";
export default {
  name: "RepoIssues",
  components: {
    IssueComments,
  },
  // PROPS
  props: {
    owner: {
      type: String,
      required: true,
    },
    repo: {
      type: String,
      required: true,
    },
  },
  // DATA
  data() {
    return {
      issues: [],
      showIssues: false,
    };
  },
  // MIXINS
  mixins: [octokitMixin],
  // METHODS
  methods: {
    async getRepoIssues(owner, repo) {
      if (typeof owner !== "string" || typeof repo !== "string") {
        return;
      }
      const octokit = this.createOctokitClient();
      const { data: issues } = await octokit.issues.listForRepo({
        owner,
        repo,
      });
      this.issues = issues;
    },
  },
  // WATCH
  watch: {
    owner: {
      immediate: true,
      handler(val) {
        this.getIssueComments(val, this.repo);
      },
      repo: {
        immediate: true,
        handler(val) {
          this.getIssueComments(this.owner, val);
        },
      },
    },
  },
};
</script>

<style>
</style>
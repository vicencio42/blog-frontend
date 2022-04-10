<template>
  <div class="home">
    <h1>Post Info</h1>
    <p>Title: {{ post.title }}</p>
    <p>Body: {{ post.body }}</p>
    <img v-bind:src="post.image" v-bind:alt="post.title" />
    <br />
    <router-link to="/posts">Back to All Posts</router-link>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get(`/posts/${this.$route.params.id}`).then((response) => {
      this.post = response.data;
    });
  },
};
</script>

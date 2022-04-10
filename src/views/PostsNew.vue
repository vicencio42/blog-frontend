<template>
  <div class="home">
    <h1>New Post</h1>
    <form v-on:submit.prevent="createPost()">
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      Title:
      <input type="text" v-model="newPost.title" />
      Body:
      <input type="text" v-model="newPost.body" />
      Image:
      <input type="text" v-model="newPost.image" />
      <input type="submit" value="Create Post" />
    </form>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newPost: {},
      errors: [],
    };
  },
  created: function () {},
  methods: {
    createPost: function () {
      axios
        .post("/posts", this.newPost)
        .then((response) => {
          console.log("new posts", response);
          this.$router.push("/posts");
        })
        .catch((error) => {
          console.log("new posts error", error.response);
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>

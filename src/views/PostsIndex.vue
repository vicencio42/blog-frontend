<template>
  <div class="home row">
    <h1 v-bind:class="className">{{ message }} count: {{ posts.length }}</h1>
    <div
      class="col"
      v-bind:class="{ selected: post === currentPost }"
      v-for="post in posts"
      v-bind:key="post.id"
      v-on:click="currentPost = post"
    >
      <div class="card" style="width: 18rem"></div>
      <img v-bind:src="post.image" class="card-img-top" v-bind:key="post.id" />
      <div class="card-body">
        <h2 class="card-title">{{ post.title }}</h2>
        <p class="card-body">{{ post.body }}</p>

        <br />
        <router-link v-bind:to="`/posts/${post.id}`" class="btn btn-primary">Show Info</router-link>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data: function () {
    return {
      message: "My Posts,",
      posts: [],
      currentPost: {},
    };
  },
  created: function () {
    this.indexPosts();
  },
  methods: {
    indexPosts() {
      axios.get("/posts").then((response) => {
        console.log(response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>
<style>
.selected .card-body {
  color: white;
  background-color: royalblue;
}
img {
  height: 450px;
  width: 250px;
  object-fit: cover;
}
</style>

<template>
  <div class="home">
    <AddPost />
    <!-- customHtml tags -->
    <PostList v-bind:posts="posts" />
  </div>
</template>

<script>
import axios from "axios";
// @ is an alias to /src
import AddPost from "@/views/AddPost.vue";
import PostList from "@/views/PostList.vue";
export default {
  name: "home",
  components: { AddPost, PostList },
  data() {
    return {
      posts: [],
      errors: []
    };
  },
  created() {
    axios
      .get(`https://jsonplaceholder.typicode.com/posts?_limit=5`)
      .then(res => {
        this.posts = res.data;
      })
      .catch(e => {
        this.errors.push(e);
      });
  }
};
</script>

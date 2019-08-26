<template>
  <div class="home">
    <AddPost v-on:add-post="addPost" />
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
  methods: {
    addPost(newPost) {
      const { title, body } = newPost;
      axios
        .post(`https://jsonplaceholder.typicode.com/posts`, {
          title: title,
          body: body
        })
        .then()
        .catch();
    }
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

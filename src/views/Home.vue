<template>
  <div class="home">
    <AddPost v-on:add-post="addPost" />
    <!-- customHtml tags -->
    <PostList v-on:del-post="deletePost" v-bind:posts="posts" />
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
          title,
          body
        })
        .then(res => (this.posts = [...this.posts, res.data]))
        .catch(err => console.log("error", err));
    },
    deletePost(id) {
      axios
        .delete(`https://jsonplaceholder.typicode.com/posts/${id}`)
        .then(res=>{
          this.posts = this.posts.filter(post=>post.id !=id)
        })
        .catch(e => {
          console.log(e);
        });
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

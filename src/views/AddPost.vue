<template>
  <div class="add-post">
    <div class="row mb-3">
      <div class="col text-right">
        <button class="btn btn-primary" v-on:click="formShow">Create new post</button>
      </div>
    </div>
    <div class="card bg-dark mb-3" v-if="formDiv">
      <div class="card-body">
        <form @submit.prevent="addPost">
          <div class="form-group">
            <label>Post title</label>
            <input
              v-model="title"
              type="text"
              name="title"
              class="form-control"
              placeholder="Enter post title"
            />
          </div>
          <div class="form-group">
            <label>Post detail</label>
            <textarea
              v-model="body"
              name="body"
              class="form-control"
              placeholder="Enter post detail"
            ></textarea>
          </div>
          <div class="row">
            <div class="col-6 mx-auto">
              <button class="btn btn-block btn-success">Create post</button>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "AddPost",
  data() {
    return {
      formDiv: false,
      title: "",
      body: ""
    };
  },
  methods: {
    formShow() {
      this.formDiv = true;
    },
    addPost() {
      const newPost = {
        title: this.title,
        body: this.body
      };
      //send up to prevent
      this.$emit("add-post", newPost);
      (this.title = ""), (this.body = "");
    }
  }
};
</script>

<style  scoped>
</style>
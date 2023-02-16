<template>
  <div>
    <h1> {{ post.body }}</h1>
    <div :key="this.commentss.id" v-for="comment in this.commentss">
      <div style="border-style: solid; margin: 2%; padding: 10px;">
        <h3>Name: {{ comment.name }}</h3>
        <h4>Email: {{ comment.email }}</h4>
        <h5>{{ comment.body }}</h5>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Post",
  data() {
    return {
      commentss: [],
    };
  },
  props: {
    post: Object,
  },
  methods: {
    async fetchComments() {
      const res = await fetch(
        `https://jsonplaceholder.typicode.com/comments?postId=${this.post.id}`
      );
      const data = await res.json();
      this.commentss = data;
    },
  },
  async created() {
    await this.fetchComments();
  },
};
</script>

<style scope>
.post {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.post h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>

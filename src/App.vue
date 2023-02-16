<template>
  <div>
    <!-- Modal, który wyświetla szczegóły wybranego postu -->
    <Modal :post="post" @closeModal="closeModal" :show.sync="showModal" />

    <div class="container">
      <!-- Nagłówek strony -->
      <Header title="Posts:" @inputText="searchPost" />
      <!-- Lista postów -->
      <Posts
        :posts="posts"
        :seachString="seachString"
        @currentPost="checkId"
        @morePosts="showMorePosts"
        @lessPosts="showPastPosts"
      />
    </div>
  </div>
</template>

<script>
import Header from "./components/Header";
import Posts from "./components/Posts.vue";
import Modal from "./components/Modal.vue";

export default {
  name: "App",
  components: {
    Header,
    Posts,
    Modal,
  },
  data() {
    return {
      posts: [],
      post: {},
      showModal: false,
      start: 0,
      seachString: "",
    };
  },
  methods: {
    async searchPost(e) {
      let condition = false;
      if (e.length >= 3) {
        condition = true;
        this.seachString = e;
        this.fetchPosts(condition);
      } else {
        this.seachString = "";
        this.fetchPosts(condition);
      }
    },
    closeModal() {
      this.showModal = false;
    },
    showMorePosts(x) {
      if (this.start < 96) {
        this.start += x;
        this.fetchPosts();
      } else alert("No more new posts");
    },
    showPastPosts(x) {
      if (this.start >= 6) {
        this.start -= x;
        this.fetchPosts();
      } else alert("U are on 1st page of posts");
    },
    checkId(id) {
      this.post = id;
      this.showModal = true;
    },
    async fetchPosts(condition = false) {
      let data;
      if (condition === false) {
        const res = await fetch(
          `https://jsonplaceholder.typicode.com/posts?_start=${this.start}&_limit=6`
        );
        data = await res.json();
        this.posts = data;
      } else {
        const res = await fetch(`https://jsonplaceholder.typicode.com/posts`);
        const allData = await res.json();
        const filtredData = allData.filter((post) =>
          post.title.toLowerCase().includes(this.seachString.toLowerCase())
        );
        data = filtredData;
        this.posts = data;
      }

      for (let z = 0; z < data.length; z++) {
        const res2 = await fetch(
          `https://jsonplaceholder.typicode.com/comments?postId=${data[z].id}`
        );
        const data2 = await res2.json();
        this.posts[z].comments = data2.length;
      }
    },
  },
  async created() {
    this.fetchPosts(false);
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
  background-color: #85868d;
}
.container {
  background-color: lightgrey;
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>

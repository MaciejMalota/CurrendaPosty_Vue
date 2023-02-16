<template>
  <div
    :key="post.id"
    v-for="post in posts"
    style="
      padding: 10px;
      border-style: solid;
      margin: 10px;
      align-items: center;
    "
    @click="this.$emit('currentPost', post)"
  >
    <p style="margin: 5px; font-size: 20px; font-weight: bold; flex-grow: 4">
      {{ post.title }}
    </p>

    <div
      style="display: flex; justify-content: space-between; margin-top: 10px"
    >
      <p style="align-self: flex-end">Post comments: {{ post.comments }}</p>
    </div>
  </div>
  <h3 v-if="this.posts.length == 0">There is no such a post to be found</h3>
  <Button
    v-if="this.seachString.length < 3"
    text="Past posts"
    color="pink"
    @btn-click="$emit('lessPosts', 6)"
  />
  <Button
    v-if="this.seachString.length < 3"
    text="Load new posts"
    color="pink"
    @btn-click="$emit('morePosts', 6)"
  />
</template>

<script>
import Button from "./Button";

export default {
  name: "Posts",
  props: {
    posts: Array,
    seachString: String,
  },
  components: {
    Button,
  },

  emits: ["currentPost", "morePosts", "lessPosts"],
};
</script>

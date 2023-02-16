<template>
  <div class="modal" v-if="show">
    <div class="modal-background" @click="close"></div>
    <div class="modal-content">
      <Post :post="post" />

    </div>
    <button class="modal-close is-large" @click="close"></button>
  </div>
</template>

<script>
import Post from './Post.vue';


  export default {
    components:{
        Post
    },

    props: {
      show: {
        type: Boolean,
        required: true,
      },
      post: Object
    },
    methods: {
      close() {
        this.$emit('closeModal');
      },

  }
};
</script>

<style>
.modal {
  position: fixed;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  z-index: 999;
  display: flex;
  align-items: center;
  justify-content: center;
}

.modal-background {
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background-color: rgba(0, 0, 0, 0.5);
}

.modal-content {
  position: relative;
  background-color: #fff;
  border-radius: 0.25rem;
  padding: 1.5rem;
  max-width: 40rem;
  max-height: 80%;
  overflow-y: auto;
}

.modal-close {
  position: absolute;
  top: 0.5rem;
  right: 0.5rem;
  background-color: transparent;
  border: none;
  font-size: 1.5rem;
  cursor: pointer;
  opacity: 0.3;
  transition: opacity 0.2s;
}

.modal-close:hover {
  opacity: 1;
}
</style>

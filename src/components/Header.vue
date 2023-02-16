<template>
  <header>
    <h1>{{ title }}</h1>
    <input
      placeholder="Search"
      type="text"
      @input="checkInput"
      style="font: 1.14em sans-serif"
    />
  </header>
</template>

<script>
export default {
  name: "Header",
  props: {
    title: String,
  },
  components: {},
  methods: {
    checkInput(e) {
      this.$emit("inputText", e.target.value);
    },
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>

<template>
  <div>
    <label for="searchField">Youtube Search: </label><br />
    <input @input="onInput" id="searchField" />
  </div>
</template>
<script>
export default {
  name: "SearchBar",
  data() {
    return { searchTerm: "", lastSearch: "" };
  },
  methods: {
    onInput(event) {
      this.$emit("termChange", event.target.value);
    },
  },
};
</script>

<style scoped>
input {
  width: 75%;
}
div {
  text-align: center;
  margin: 20px;
}
</style>
<template>
  <form v-on:submit.prevent="filterSubmit()" class="" action="#" method="post>
    <button type="submit" name="filterButton">Toggle</button>
  </form>
</template>

<template>
  <form v-on:submit.prevent="bookSubmit(bookData)" class="" action="#" method="post">
    <input v-model=bookData.bookTitle type="text" name="title" value="" placeholder="Book Title">
    <input v-model=bookData.bookAuthor type="text" name="author" value="" placeholder="Book Author">
    <div>
      <input v-model=bookData.finishedReading type="checkbox" name="finishedReading">
      <label for="finishedReading">Finished Reading</label>
    </div>
    <div>
      <input v-model=bookData.ownership type="radio" value="borrowed" name="borrowed">
      <label for="borrowed">Borrowed</label>
      <input v-model=bookData.ownership type="radio" value="bought" name="bought">
      <label for="bought">Bought</label>
    </div>
    <button type="submit" name="button">Add Book</button>
  </form>
</template>

<script>
export default {
  name: "BookForm",
  props: ["books"],
  data() {
    return {
      bookData: {
        bookTitle: "",
        bookAuthor: "",
        finishedReading: false,
        ownership: []
        }
    };
  },
  methods: {
    filterSubmit() {
      this.$emit("filterSubmit")
    },
    bookSubmit(bookData) {
      this.$emit("addBook", bookData)
    }
  }
};
</script>

<style>
</style>

<template>
  <form ref="bookform" v-on:submit.prevent="bookSubmit(bookData)" class="" action="#" method="post">
    <input v-model=bookData.bookTitle type="text" name="title" value="" placeholder="Book Title">
    <input v-model=bookData.bookAuthor type="text" name="author" value="" placeholder="Book Author">
    <div>
      <input v-model=bookData.finishedReading type="radio" value="read" name="read">
      <label for="read">Read</label>
      <div v-if="bookData.finishedReading === 'read'">
        <input v-model=bookData.liked type="checkbox" name="liked">
        <label for="liked">Liked the book</label>
      </div>
      <input v-model=bookData.finishedReading type="radio" value="not read" name="notread">
      <label for="notread">Not Read</label>
      <input v-model=bookData.finishedReading type="radio" value="reading" name="reading">
      <label for="reading">Reading</label>
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
        finishedReading: "",
        liked: false,
        ownership: []
        }
    };
  },
  methods: {
    bookSubmit(bookData) {
      this.$emit("addBook", bookData);
      Object.keys(bookData).forEach(v => bookData[v] = "");
    }
  }
};
</script>

<style>
</style>

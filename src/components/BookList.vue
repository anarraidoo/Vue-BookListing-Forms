<template>
  <div>
    <h1>{{title}}</h1>
    <input v-model=searchInput type="text" placeholder="Search Books">
    <ul>
      <book-item v-for='book in searchedBooks' :key='book.id' :book='book'></book-item>
    </ul>
    <hr>
    <button class="ui button toggle" @click='changeFilterType'>{{filterType ? 'Book State' : 'Ownership'}}</button>
    <span v-if="filterType">
      <h2>Filtered Books By Ownership</h2>
      <select v-model="holding">
        <option v-for="filter in ownershipFilters">{{ filter }}</option>
      </select>
      <ul>
        <book-item v-for='book in filteredBooks' :key='book.id' :book='book'></book-item>
      </ul>
    </span>
    <span v-else>
      <h2>Filtered Books By Book State</h2>
      <select v-model="status">
        <option v-for="filter in statesFilters">{{ filter }}</option>
      </select>
      <ul>
        <book-item v-for='book in filteredBooks' :key='book.id' :book='book'></book-item>
      </ul>
    </span>
    <br><hr>
    <book-form @addBook='appendBook'></book-form>
  </div>
</template>

<script>
import _ from "lodash";
import BookItem from "./BookItem";
import BookForm from "./BookForm";

export default {
  name: "BookList",
  data() {
    return {
      title: "My Book Library",
      books: [
        { title: "Dom Juan", author: "Molière", finishedReading: "read", ownership: "bought", liked: true },
        { title: "La Ballade de Sammy Song", author: "Marie-Agnès Vermande-Lhern", finishedReading: "read", ownership: "borrowed", liked: true },
        { title: "The Bridgertons Happily Ever After", author: "Julia Quinn", finishedReading: "not read", ownership: "bought", liked: false },
        { title: "(You) Set Me on Fire", author: "Mariko Tamaki", finishedReading: "reading", ownership: "bought", liked: false },
        { title: "Le Vrai Monde?", author: "Michel Tremblay", finishedReading: "read", ownership: "bought", liked: true },
        { title: "Burry Me Deep", author: "Christopher Pike", finishedReading: "read", ownership: "borrowed", liked: true },
        { title: "Who Made Me a Princess", author: "Plutus", finishedReading: "read", ownership: "borrowed", liked: false }
      ],
      ownershipFilters: ["bought", "borrowed"],
      statesFilters: ["read", "not read", "reading"],
      holding: "bought",
      status: "read",
      filterType: true,
      searchInput: ""
    };
  },
  computed: {
    filteredBooks() {
      if (this.filterType) {
        return _.filter(this.books, ["ownership", this.holding]);
      } else {
        return _.filter(this.books, ["finishedReading", this.status]);
      }
    },
    searchedBooks() {
      const searchFilter = book => {
        return book.title.toLowerCase().match(this.searchInput.toLowerCase());
      };
      return _.filter(this.books, searchFilter);
    }
  },
  components: {
    BookItem,
    BookForm
  },
  methods: {
    appendBook(bookData) {
      this.books.push({ title: bookData.bookTitle, author: bookData.bookAuthor, finishedReading: bookData.finishedReading,
                        ownership: bookData.ownership, liked: bookData.liked });
    },
    changeFilterType() {
      this.filterType = !this.filterType;
    }
  }
};
</script>

<style>
h1,
h2 {
  font-weight: normal;
}
ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: block;
  margin: 0 10px;
}
</style>

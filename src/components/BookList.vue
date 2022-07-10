<template>
  <div>
    <h1>{{title}}</h1>
    <input v-model=searchInput type="text" placeholder="Search Books">
    <ul>
      <book-item v-for='book in searchedBooks' :key='book.id' :book='book'></book-item>
    </ul>
    <hr>
    <book-form @filterButton='filterSubmit'></book-form>
    <span v-if="filterSelected">
      <h2>Filtered Books By Ownership</h2>
      <select v-model="holding">
        <option v-for="filter in ownershipFilters">{{ filter }}</option>
      </select>
      <ul>
        <book-item v-for='book in filteredBooks' :key='book.id' :book='book'></book-item>
      </ul>
    </span>
    <span v-else>
      <h2>Filtered Books By States</h2>
      <select v-model="holding">
        <option v-for="filter in ownershipFilters">{{ filter }}</option>
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
      title: "All Books",
      states: ["Want to Read", "Read", "Reading"],
      books: [
        { title: "Dom Juan", author: "Molière", finishedReading: true, ownership: "bought" },
        { title: "La Ballade de Sammy Song", author: "Marie-Agnès Vermande-Lhern", finishedReading: true, ownership: "borrowed"  },
        { title: "The Bridgertons Happily Ever After", author: "Julia Quinn", finishedReading: false, ownership: "bought"  },
        { title: "(You) Set Me on Fire", author: "Mariko Tamaki", finishedReading: false, ownership: "bought"  },
        { title: "Le Vrai Monde?", author: "Michel Tremblay", finishedReading: true, ownership: "bought"  },
        { title: "Burry Me Deep", author: "Christopher Pike", finishedReading: true, ownership: "borrowed"  }
      ],
      ownershipFilters: ["bought", "borrowed"],
      statesFilters: ["read", "not read", "want to Read", "reading"],
      holding: "bought",
      filterSelected: true,
      searchInput: ""
    };
  },
  computed: {
    filteredBooks() {
      return _.filter(this.books, ["ownership", this.holding]);
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
                        ownership: bookData.ownership });
    },
    selectFilter() {
      this.filterSelected = !filterSelected;
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

<script >
import Header from './components/Header.vue'
import Results from './components/Results.vue'
import Search from './components/Search.vue'
import booksData from '@/data.json'
export default{
  components: {
    Header,
    Results,
    Search
  },
  data() {
    return {
      books: booksData,
      searchText: "",
      searchYears: "",
      searchPages: "",
      isOpen: false
    }
  },
  methods: {
    filterBooks(){
      // only selects books where title or author match the searchText, pages, and year
      return this.books.filter((book) =>
      (book.title.toLowerCase().includes(this.searchText.toLowerCase()) ||
      book.author.toLowerCase().includes(this.searchText.toLowerCase()) )
      && this.matchPages(book)
      && this.matchYears(book)
      );
    },
    matchPages(book){
      if (this.searchPages == "Less than 200 pages" && book.pages > 200) {
        return false
      } 
      else if (this.searchPages == "200 to 400 pages" && (book.pages <= 200 || book.pages > 400)) {
        return false
      }
      else if (this.searchPages == "Greater than 400 pages" && book.pages <= 400){
        return false
      }
      else {
        return true
      }
    },
    matchYears(book){
      if (this.searchYears == "before" && book.year >= 1900) {
        return false
      }
      else if (this.searchYears == "after" && book.year < 1900){
        return false
      }
      else {
        return true
      }
    }
  }
}
</script>

<template>
  <content class="has-navbar-fixed-top">
    <!-- ----------NAVBAR-------------- -->
    <section class="section">
      <div class="navbar is-transparent is-fixed-top is-light is-spaced" role="navigation" aria-label="main navigation">
        <div class="navbar-brand">
          <Header/>
          <a role="button" class="navbar-burger" aria-label="menu" aria-expanded="false" @click="this.isOpen = !this.isOpen" v-bind:class="{'is-active': this.isOpen}">
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
            <span aria-hidden="true"></span>
          </a>
        </div>
        <div class="navbar-menu" v-bind:class="{'is-active': isOpen}">
          <div class="navbar-end">
            <Search 
            v-model:text="searchText" 
            v-model:pages="searchPages"
            v-model:years="searchYears"
            />
          </div>
        </div>
      </div>
    </section>
    <!-- ------------------RESULTS----------------------- -->
    <div class="is-flex is-flex-wrap-wrap is-justify-content-space-around">
      <Results :books = this.filterBooks()></Results>
    </div>
  </content>
</template>

<style>
</style>

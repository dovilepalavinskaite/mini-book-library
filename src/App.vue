<template>
  <div class="d-flex">
    <side-header @set-page="handleSetPage" />
    <home-page v-if="activePage === 'homepage'" />
    <books-list v-if="activePage === 'books-list'" />
    <books-submit-form v-if="activePage === 'books-form'" />
  </div>
</template>

<script>
import SideHeader from './components/SideHeader.vue';
import HomePage from './components/HomePage.vue';
import BooksList from './components/BooksList.vue';
import BooksSubmitForm from './components/BooksSubmitForm.vue';

export default {
  name: 'App',
  components: {
    SideHeader,
    HomePage,
    BooksList,
    BooksSubmitForm
  },
  data() {
    return {
      activePage: 'homepage'
    };
  },
  methods: {
    handleSetPage(page) {
      this.activePage = page;
    }
  }
}
</script>

<style>

* {
  box-sizing: border-box;
  margin: 0;
}
</style>

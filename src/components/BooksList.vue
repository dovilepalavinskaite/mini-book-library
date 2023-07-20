<template>
    <div>
      <div class="pl-4 pt-4">
        <h4>All My Books:</h4>
        <hr class="divider">
      </div>
      <div class="d-flex flex-wrap">
        <book-card :all-books="allBooks" />
      </div>
    </div>
</template>
  
<script>
import BookCard from './BookCard.vue';
import axios from 'axios';

  export default {
    name: 'BooksList',
    components: { BookCard },
    data() {
      return {
        allBooks: null
      }
    },
    created() {
      this.getAllBooksList();
    },
    methods: {
      getAllBooksList() {
        axios.get('https://vue-books-database-default-rtdb.firebaseio.com/books.json')
        .then(response => {
          this.allBooks = response.data;
        });
      },
    }
  }
</script>
  
<style scoped>
  .divider {
    width: 33%;
  }
</style>
  
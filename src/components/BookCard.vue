<template>
    <div v-for="(book, index) in allBooks" :key="index" class="book-card m-4">
        <div>
        <img src="../assets/book-card-cover.jpg" alt="Book card image" class="book-card-img">
        </div>
        <div class="p-2">
        <div class="d-flex justify-content-between align-items-center">
            <h5>{{ book.bookTitle }}</h5>
            <div class="d-flex align-items-center">
            <i class="fas fa-star mr-1"></i>
            <h6 class="m-0 p-0">{{ book.rating }}</h6>
            </div>
        </div>
        <h6>Author: {{ book.bookAuthor }}</h6>
        <div class="d-flex flex-wrap align-items-center">
            <div v-for="(genre, index) in book.genre" :key="index" class="genre-wrapper p-1 mr-1 mb-1">
            <p class="text-success m-0">{{ formatBookGenre(genre) }}</p>
            </div>
        </div>
        <hr>
        <p>{{ book.bookReview }}</p>
        </div>
    </div>
</template>

<script>
  export default {
    name: 'BookCard',
    props: {
        allBooks: {
        type: Array,
        required: true
        }
    },
    methods: {
      formatBookGenre(genre) {
        return genre.replace(/-/g, ' ');
      }
    }
  }
</script>

<style scoped>
  
  p {
    font-size: 12px;
  }
  h6 {
    font-size: 10px;
  }
  .book-card {
    border: 1px solid #e5e5e5;
    border-radius: 6px;
    width: 220px;
  }
  .book-card-img {
    object-fit: cover;
    width: 100%;
    border-top-left-radius: 6px;
    border-top-right-radius: 6px;
  }
  .fa-star {
    color: #ffbf00;
  }
  .genre-wrapper {
    border-radius: 30px;
    border: 1px solid #28a745;
  }
</style>
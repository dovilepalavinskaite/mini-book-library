<template>
    <div class="form-wrapper d-flex my-5">
        <div class="form-container p-4 col-12 col-md-6">
            <img src="../assets/book-form-image.jpg" alt="Book form image" class="img-banner d-block d-md-none mb-3">
            <h4>Register your Book</h4>
            <hr class="divider">
            <form>
                <div class="form-input py-2">
                    <label for="book-title" class="d-block">Book Title</label>
                    <input id="book-title" name="book-title" type="text" class="text-input" v-model="books.bookTitle" />
                </div>
                <div class="form-input py-2">
                    <label for="book-author" class="d-block">Author</label>
                    <input id="book-author" name="book-author" type="text" class="text-input" v-model="books.bookAuthor" />
                </div>
                <hr>
                <div class="form-input py-2">
                    <p>What is book genre?</p>
                    <div class="d-flex align-iems-center">
                        <input id="genre-action" name="genre" value="action-and-adventure" type="checkbox" v-model="books.genre" class="mr-2" />
                        <label for="genre-action" class="mb-0">Action and Adventure</label>
                    </div>
                    <div>
                        <input id="genre-classics" name="genre" value="classics" type="checkbox" v-model="books.genre" class="mr-2" />
                        <label for="genre-classics" class="mb-0">Classics</label>
                    </div>
                    <div>
                        <input id="genre-detective-and-mystery" name="genre" value="detective-and-mystery" type="checkbox" v-model="books.genre" class="mr-2" />
                        <label for="genre-detective-and-mystery" class="mb-0">Detective and Mystery</label>
                    </div>
                    <div>
                        <input id="genre-fantasy" name="-genre" value="fantasy" type="checkbox" v-model="books.genre" class="mr-2" />
                        <label for="genre-fantasy" class="mb-0">Fantasy</label>
                    </div>
                    <div>
                        <input id="genre-horror" name="genre" value="horror" type="checkbox" v-model="books.genre" class="mr-2" />
                        <label for="genre-horror" class="mb-0">Horror</label>
                    </div>
                    <div>
                        <input id="genre-romance" name="genre" value="romance" type="checkbox" v-model="books.genre" class="mr-2" />
                        <label for="genre-romance" class="mb-0">Romance</label>
                    </div>
                    <div>
                        <input id="genre-other" name="genre" value="other" type="checkbox" v-model="books.genre" class="mr-2" />
                        <label for="genre-other" class="mb-0">Other</label>
                    </div>
                </div>
                <hr>
                <div class="form-input py-2">
                    <label for="book-rating">How would you rate this book?</label>
                    <div class="d-flex">
                        <div v-for="star in 5" :key="star" @click="books.rating = star">
                            <i class="fa-regular fa-star" :class="{ 'fa-solid': star <= books.rating }"></i>
                        </div>
                    </div>
                </div>
                <hr>
                <div class="form-input py-2">
                    <label for="book-review">Comments about the book</label>
                    <textarea id="book-review" name="book-review" v-model="books.bookReview" />
                </div>
            </form>
            <div v-if="showSuccessMessage" class="d-flex text-success">
                <i class="fa-solid fa-circle-check mr-2"></i>
                <p>Your book was placed in the database successfully!</p>
            </div>
            <div class="d-flex justify-content-center mt-5">
                <button @click="submitForm" class="p-1">Submit</button>
            </div>
        </div>
        <div class="form-bcg">
            <img src="../assets/book-form-image.jpg" alt="Book form image" class="d-none d-md-block">
        </div>
    </div>
</template>

<script>

import axios from 'axios';
  export default {
    name: 'BooksSubmitForm',
    data() {
        return {
            books: {
                bookTitle: null,
                bookAuthor: null,
                bookReview: null,
                genre: [],
                rating: 0
            },
            showSuccessMessage: false
        }
    },
    methods: {
        submitForm() {
            axios.post('https://vue-books-database-default-rtdb.firebaseio.com/books.json', this.books)
                .then(response => {
                    if (response.status === 200) {
                        this.showSuccessMessage = true;
                        this.books.bookTitle = null;
                        this.books.bookAuthor = null;
                        this.books.bookReview = null;
                        this.books.genre = [];
                        this.books.rating = 0;
                    }
                });
        }
    }
}
</script>


<style scoped>
  .form-wrapper {
    margin: 0 auto;
    width: 70%;
    border: 1px solid #e5e5e5;
    box-shadow: 0px 2px 4px rgba(0, 0, 0, 0.2);
    border-radius: 6px;
    display: flex;
  }
  .divider {
    width: 33%;
  }
  .img-banner {
    width: 100%;
    height: 50px;
  }
  img {
    object-fit: cover;
  }
  .form-bcg {
    flex: 1;
    display: flex;
    justify-content: flex-end;
  }

  .form-bcg img {
    width: 100%;
    height: auto;
    max-height: 100%;
  }
  label, p {
    font-size: 12px;
  }
  button {
    background: #09302d;
    color: #fff;
    border: 1px solid #09302d;
    max-width: 250px;
    width: 100%;
    border-radius: 6px;
    font-size: 14px;
    cursor: pointer;
  }
  button:hover {
    background: #061c1d;
  }
  textarea, .text-input {
    width: 100%;
  }
  .fa-regular {
    color: #ffbf00;
    cursor: pointer;
  }
</style>

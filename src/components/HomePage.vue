<template>
  <div>
    <div class="pl-4 pt-4 d-flex">
      <div>
        <h4>All Categories:</h4>
        <hr class="divider">
        <div class="d-flex">
          <div class="d-flex flex-wrap col-5 align-self-baseline">
            <div v-for="category in allCategories" :key="category.id" @click="changeBooksCategory(category.category)" class="category-table mr-4 mb-4 p-2 pt-4">
              <div class="pt-3 pb-2">
                <i class="fa-solid" :class="`${category.icon}`"></i>
              </div>
              {{ formatBookGenre(category.category) }}
            </div>
          </div>
          <div class="col-7">
            <h5>Chosen Category: {{ chosenCategory }}</h5>
            <div class="d-flex flex-wrap">
              <book-card :all-books="filteredCategories" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
  </template>
  
<script>
import BookCard from './BookCard.vue';
import axios from 'axios';

  export default {
    name: 'HomePage',
    components: { BookCard },
    data() {
      return {
        allBooks: null,
        chosenCategories: null,
        activeCategory: '',
        allCategories: [
          {
            id: 1,
            category: 'action-and-adventure',
            icon: 'fa-person-running'
          },
          {
            id: 2,
            category: 'classics',
            icon: 'fa-landmark'
          },
          {
            id: 3,
            category: 'detective-and-mystery',
            icon: 'fa-user-secret'
          },
          {
            id: 4,
            category: 'fantasy',
            icon: 'fa-hat-wizard'
          },
          {
            id: 5,
            category: 'horror',
            icon: 'fa-ghost'
          },
          {
            id: 6,
            category: 'romance',
            icon: 'fa-heart'
          },
          {
            id: 7,
            category: 'other',
            icon: 'fa-book'
          },
          {
            id: 8,
            category: 'none',
            icon: 'fa-x'
          }
        ]
      }
    },
    created() {
      this.getAllBooksList();
    },
    computed: {
      filteredCategories() {
        return this.chosenCategories !== null ? this.chosenCategories : this.allBooks;
      },
      chosenCategory() {
        return this.activeCategory.length ? this.activeCategory.replace(/-/g, ' ') : 'none';
      }
    },
    methods: {
      getAllBooksList() {
        axios.get('https://vue-books-database-default-rtdb.firebaseio.com/books.json')
        .then(response => {
          this.allBooks = response.data;
        });
      },
      formatBookGenre(genre) {
        const capitalizedGenre = genre.charAt(0).toUpperCase() + genre.slice(1);
        const formattedGenre = capitalizedGenre.replace(/-/g, ' ');
        return formattedGenre;
      },
      getBooksByCategory(category) {
        if (category === 'none') {
          this.chosenCategories = null; // Clear the chosenCategories
          return this.allBooks; // Return the entire books object
        }

        const booksArray = Object.values(this.allBooks);
        this.chosenCategories = booksArray.filter((book) => book.genre.includes(category));
      },
      changeBooksCategory(category) {
        this.activeCategory = category;
        this.getBooksByCategory(this.activeCategory);
      }
    }
}
</script>
  
<style scoped>

.divider {
    width: 33%;
  }
.category-table {
  height: 160px;
  width: 160px;
  border-radius: 6px;
  color: #aebac4;
  cursor: pointer;
  box-shadow: -2px 9px 14px 3px rgba(207,188,188,0.75);
  -webkit-box-shadow: -2px 9px 14px 3px rgba(207,188,188,0.75);
  -moz-box-shadow: -2px 9px 14px 3px rgba(207,188,188,0.75);
}
.category-table:hover {
  -ms-transform: scale(1.1);
  -webkit-transform: scale(1.1);
  transform: scale(1.1); 
}
.fa-solid {
  font-size: 38px;
}
</style>
  
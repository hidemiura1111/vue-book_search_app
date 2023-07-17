<template>
  <v-app>
    <HeaderComponent @delete-local-storage="deleteLocalStorage"/>
      <v-main>
        <v-container>
          <router-view
            :books="books"
            @add-book-list="addBook"
            @update-book-info="updateBookInfo"
            @remove-book="removeBook"
          />
        </v-container>
      </v-main>
    <FooterComponent/>
  </v-app>
</template>

<script>
import HeaderComponent from '@/global/HeaderComponent';
import FooterComponent from '@/global/FooterComponent';
const STORAGE_KEY = 'books';

export default {
  name: 'App',
  components: {
    HeaderComponent,
    FooterComponent,
  },
  data() {
    return {
      books: [],
      newBook: null,
    };
  },
  mounted() {
    if (localStorage.getItem(STORAGE_KEY)) {
      try {
        this.books = JSON.parse(localStorage.getItem(STORAGE_KEY));
      } catch(e) {
        localStorage.removeItem(STORAGE_KEY);
      }
    }
  },
  methods: {
    addBook(e) {
      this.books.push({
        id: this.books.length ? this.books.slice(-1)[0].id + 1 : 0,
        title: e.title,
        image: e.image,
        description: e.description,
        readDate: '',
        memo: '',
      });
      this.saveBooks();
      this.$router.push('/');
    },
    removeBook(targetBook) {
      const bookIndex = this.books.findIndex(book => book.id === targetBook.id);
      const isDelete = `Remove "${targetBook.title}"?`
      if (window.confirm(isDelete)) {
        this.books.splice(bookIndex, 1);
        this.saveBooks();
      }
    },
    saveBooks() {
      const parsed = JSON.stringify(this.books);
      localStorage.setItem(STORAGE_KEY, parsed);
    },
    updateBookInfo(e) {
      const bookIndex = this.books.findIndex(book => book.id === e.id);
      const book = this.books.find(book => book.id === e.id);
      const updateInfo = {
        id: e.id,
        readDate: e.readDate,
        memo: e.memo,
        title: book.title,
        image: book.image,
        description: book.description,
      };
      this.books.splice(bookIndex, 1, updateInfo);
      this.saveBooks();
      this.$router.push('/');
    },
    gotoEditPage(id) {
      this.$router.push(`/edit/${id}`);
    },
    deleteLocalStorage() {
      const isDelete = 'Delete all?'
      if (window.confirm(isDelete)) {
        localStorage.setItem(STORAGE_KEY, '') // Not necessary
        localStorage.removeItem(STORAGE_KEY)
        this.books = []
        window.location.reload()
      }
    }
  }
};
</script>

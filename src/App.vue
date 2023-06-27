<template>
  <v-app>
    <HeaderComponent/>
      <v-main>
        <v-container>
          <router-view
            :books="books"
            @add-book-list="addBook"
            @update-book-info="updateBookInfo"
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
        id: this.books.length + 1,
        title: e.title,
        image: e.image,
        description: e.description,
        readDate: '',
        memo: '',
      });
      this.saveBooks();
      this.gotoEditPage(this.books.slice(-1)[0].id);
    },
    removeBook(x) {
      this.books.splice(x, 1);
      this.saveBooks();
    },
    saveBooks() {
      const parsed = JSON.stringify(this.books);
      localStorage.setItem(STORAGE_KEY, parsed);
    },
    updateBookInfo(e) {
      const updateInfo = {
        id: e.id,
        readDate: e.readDate,
        memo: e.memo,
        title: this.books[e.id - 1].title,
        image: this.books[e.id - 1].image,
        description: this.books[e.id - 1].description,
      };
      this.books.splice(e.id - 1, 1, updateInfo);
      this.saveBooks();
      this.$router.push('/');
    },
    gotoEditPage(id) {
      this.$router.push(`/edit/${id}`);
    },
  }
};
</script>

<template>
  <div>
    <v-row>
      <v-col cols="12">
        <v-card class="mx-auto">
          <v-row>
            <v-col cols="4">
              <v-img :src="book?.image"></v-img>
            </v-col>
            <v-col cols="8">
              <v-card-title>
                Title: {{ book?.title }}
              </v-card-title>

              Date Read:
              <v-menu
                v-model="menu"
                :close-on-content-click="false"
                :nudge-right="40"
                transition="scale-transition"
                offset-y
                min-width="auto"
              >
                <template v-slot:activator="{ on, attrs }">
                  <v-text-field
                    v-model="date"
                    readonly
                    v-bind="attrs"
                    v-on="on"
                  ></v-text-field>
                </template>
                <v-date-picker
                  v-model="date"
                  @input="menu = false"
                ></v-date-picker>
              </v-menu>

              Impressions:
              <v-textarea
                class="mx-2" v-model="book.memo"
              >
                {{ book?.memo }}
              </v-textarea>

              <v-card-actions>
                <v-btn color="secondary" to="/">Book Index</v-btn>
                <v-btn color="info" @click="updateBookInfo">Store</v-btn>
              </v-card-actions>
            </v-col>
          </v-row>
        </v-card>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  name: 'BookEdit',
  props: {
    books: {
      type: Array,
      required: false,
    },
  },
  data() {
    return {
      book: '',
      date: new Date().toISOString().substr(0, 10),
      menu: false,
    }
  },
  watch: {
    books: {
      immediate: true,
      handler() {
        this.book = this.books[this.$route.params.id];
        if (this.book.readDate) {
          this.date = this.book.readDate;
        } else {
          this.date = new Date().toISOString().substr(0, 10);
        }
      }
    }
  },
  methods: {
    updateBookInfo() {
      this.$emit('update-book-info', {
        id: this.book.id,
        readDate: this.date,
        memo: this.book.memo,
      })
    }
  },
  // beforeRouteEnter (to, from, next) {
  //   next(vm => {
  //     vm.$nextTick(() => {
  //       console.log(vm.books);
  //       vm.book = vm.books[vm.$route.params.id];
  //     });
  //   });
  // }
}
</script>

<style>

</style>
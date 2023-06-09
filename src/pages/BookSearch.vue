<template>
  <div>
    <v-container>
      <v-row>
        <v-col cols="6">
          <v-text-field
            v-model="keyword"
            label="Search Book Titile"
          ></v-text-field>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="3">
          <v-btn
            color="primary"
            @click="search(keyword)"
          >
          Search
          </v-btn>
        </v-col>
        <v-col cols="3">
          <v-btn
            color="secondary"
            to="/"
          >
            Index
          </v-btn>
        </v-col>
      </v-row>
      <v-row>
        <v-col
          cols="12"
          md="6"
          v-for="(book, index) in searchResults" :key="book.index"
        >
          <v-card class="mx-auto">
            <v-row>
              <v-col cols="2">
                <v-img :src="book.img"/>
              </v-col>
              <v-col cols="10">
                <v-card-title>{{ book.title }}</v-card-title>
                <v-card-text>{{ book.description }}</v-card-text>
                <v-spacer></v-spacer>
                <v-card-actions>
                  <v-btn fab dark color="indigo"
                    @click="addBookList(index)"
                  >
                    <v-icon>mdi-plus</v-icon>
                  </v-btn>
                </v-card-actions>
              </v-col>
            </v-row>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </div>
</template>

<script>
export default {
  name: 'BookSearch',
  data() {
    return {
      keyword: '',
      searchResults: []
    }
  },
  methods: {
    async search(keyword) {
      this.searchResults = []

      // Crate query string
      const baseUrl = 'https://www.googleapis.com/books/v1/volumes?';
      const params = {
        q: `intitle:${keyword}`,
        maxResults: 10
      }
      const queryString = new URLSearchParams(params)

      // Fetch data from Google Books API
      const response = await fetch(baseUrl + queryString)
      .then(response => response.json())

      // Push data to searchResult
      for (let book of response.items) {
        let title = book.volumeInfo.title
        let img = book.volumeInfo.imageLinks.thumbnail
        let description = book.volumeInfo.description
        this.searchResults.push({
          title: title ? title : 'No title',
          img: img ? img : 'https://placehold.jp/150x200.png',
          description: description ? description.slice(0, 40) : 'No description'
        })
      }
      console.log(this.searchResults)
    }
  }
}
</script>

<style>

</style>
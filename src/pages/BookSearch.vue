<template>
  <div>
    <v-container>
      <v-row>
        <v-vol cols="6">
          <v-text-field
            v-model="keyword"
            label="Search Book Titile"
          ></v-text-field>
        </v-vol>
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
    </v-container>
  </div>
</template>

<script>
export default {
  name: 'BookSearch',
  data() {
    return {
      keyword: '',
      searchResult: []
    }
  },
  methods: {
    async search(keyword) {
      this.searchResult = []

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
        this.searchResult.push({
          title: title ? title : 'No title',
          img: img ? img : 'https://placehold.jp/150x200.png',
          description: description ? description.slice(0, 40) : 'No description'
        })
      }
    }
  }
}
</script>

<style>

</style>
<template>
  <div>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-spacer></v-spacer>
      <v-btn
        color="error"
        @click="deleteLocalStorage"
      >
        Delete All
      </v-btn>
    </v-app-bar>
  </div>
</template>

<script>
export default {
  name: 'HeaderComponent',
  methods: {
    deleteLocalStorage() {
      this.$emit('delete-local-storage')
    }
  }

}
</script>

<style>

</style>